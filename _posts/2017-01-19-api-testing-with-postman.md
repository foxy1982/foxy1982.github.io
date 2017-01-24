---
author: danfox1982
comments: true
date: 2017-01-23 08:34:30+00:00
layout: post
slug: api-testing-with-postman
title: API Testing With Postman
tags: [Coding, Testing]
image:
  feature: banner.jpg
---

[Postman](https://www.getpostman.com/){:target="_blank"} is an absolutely brilliant tool for ad-hoc API testing.  It’s really easy to send requests to endpoints regardless of whether they need headers, what the HTTP verb is, or what the payload structure is like.

Now that functionality is great on its own, but the environments make it even better.  Now I can change the URL or a header value to be a variable which I can change depending on which environment I'm talking to.  Want to see what the same query looks like against test or prod?  Easy, just change environment and Postman will replace the variable value for you!

![Environments]({{ site.assets_url }}/images/postman-environments.jpg)

For months I used those two features of Postman and thought it was a brilliant tool… and then I discovered the test engine that sits quietly under the hood, waiting until you spot the “Tests” tab.  Tests can be specified in JavaScript, so a line like this:

`tests["Status code is 201"] = responseCode.code === 201;`

would simply make sure that the response code was 201.  Definitely better than manually checking the response code in Postman.  Handily it even has some snippets to help you write the JavaScript if you’re not familiar with the syntax.  You can easily check headers, body content or response times.

Often you’ll want to test a complex interaction with an API by making multiple calls and using the returned data from the first request in subsequent calls.  That can be done too, using the power of the environments I mentioned earlier.  I’m going to use my [Snooker Scorer](https://github.com/foxy1982/snooker-scorer-2){:target="_blank"} example for this as it has exactly the kind of interaction I’m talking about.  Import the test collection and environment file (in the `tests` folder) into Postman to have a look.  The `snooker` environment will be pointing to my deployed server so the tests should run straight away (by substituting the environment variable `host` in the request URLs with my server address).

To create a new game, you `POST` some data to the API, and this returns the game ID.  There are a couple of assertions which check the HTTP status code and that the response has an ID.

The next endpoint to test is to get the status of the game we just created, so we'll need that ID again, which is easy in Postman.  Since the “Tests” script is JavaScript, you can write more than just assertions... you can also set an environment variable which will persist in the current session for that environment.  This is done with `postman.setEnvironmentVariable`

![Tests tab]({{ site.assets_url }}/images/postman-tests-tab.jpg)

After the assertions, the test script for the first request does this:

```
var postResponse = JSON.parse(responseBody);
postman.setEnvironmentVariable("gameId", postResponse.id);
```

which pulls the ID out of the response and sets it in `gameId` in the environment.  In the second request, you can see that the URL includes this `gameId` variable:

{% raw %}
`http://{{host}}:1147/game/{{gameId}}`
{% endraw %}

Postman will insert the `gameId` into the URL in the same way as it sets the `host` for us.  Again, the test scripts do assertions.  We now set a player ID variable to use in subsequent tests.  If you want to reorder tests, I just drag them around in the left-hand pane... but note that any tests which depend on environment variables being set in earlier tests are going to fail... alternatively you can force Postman to jump to a certain request using `postman.setNextRequest("POST shot");`

So what we have now is great.  I can open up Postman, pick a collection, and click each request in turn and watch the tests report green each time.  However if there is a lot of tests this can be a pain, and if I click them out of order by accident, I’m invalidating all the testing since the environment variables persist in the session and may alter the behaviour of the requests.

Enter the Test Runner!  You can launch the test runner by clicking the small arrow next to the collection name, and then clicking "Run".

![Tests tab]({{ site.assets_url }}/images/postman-test-runner-button.jpg)

This magical little window make this so much easier.  I simply choose an environment, choose how many times to run the tests and click Start Test.  Each request is executed, then the test script is run (including setting variables for the next request), then move on to the next call.

![Tests tab]({{ site.assets_url }}/images/postman-test-runner-window.jpg)

Let’s just take stock of where we are.  Given a couple of JSON files (one for the collection, one for the environment), I can import these into Postman, and by using the test runner I can get a full set of results based on those files.  That sounds like something that could be done via command line, so I could add it to a deployment pipeline… Great news!  You can!

Enter Newman!

[Newman](https://www.getpostman.com/docs/newman_intro){:target="_blank"} is a NodeJS package that will execute the collection for you and output the results to command line or to a file.  Install NodeJS if you don't have it, then run

`npm install -g newman`

You may need to start a new shell after you install this, but you should be ready to run Newman now:

```
newman run snooker-scorer.postman_collection.json
--environment snooker.postman_environment.json
```

Which will spit out something like this:

![Tests tab]({{ site.assets_url }}/images/postman-test-runner-output.jpg)

There are also file output formats available, such as json:

```
newman run snooker-scorer.postman_collection.json
--environment snooker.postman_environment.json
--reporters json
--reporter-json-export results.json
```

This is a really neat test setup which documents behaviour, is simple enough to be used by developers and non-developers with basic coding skills, and can be easily added to a development pipeline.  Enjoy!
