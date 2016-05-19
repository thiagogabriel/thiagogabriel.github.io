---
layout: post
title: "HTTPotion or HTTPoison?"
comments: true
categories:
    elixir
    phoenix
    httpotion
    httpoison
---

I'm working on an [Phoenix][phoenix] application which does external requests. My first
approach was using [HTTPotion][httpotion] 2.2.2, which looked more stable, with only 1 opened
issue on Github. After doing some benchmarks, I got surprised how different the
results are.

The application I used as example works like a proxy. If I do a POST request to
my application http://my_phoenix_app.com/1, the application does a request to
http://requestb.in/1 in another process using `spawn` and saves the result,
including the request duration, headers and body on database.

I used ab (Apache Benchmark) to test the requests and the command I used was:

{% highlight bash %}
ab -p json_file.txt -T 'application/json' -c CONCURRENCY -n REQUESTS https://myapp.herokuapp.com/api/webhooks/1
{% endhighlight %}

Where **json_file.txt** content is `{"first_name":"Jony"}` and **CONCURRENCY**
and **REQUESTS** have the values below.

### HTTPotion 2.2.2

| # | requests | concurrency | failed | requests/second |
|---|---|---|---|---|
| 1 | 2000     | 400         | 1225   | 109.46          |
| 2 | 800      | 150         | 429    | 108.48          |
| 3 | 800      | 80          | 385    | 85.14           |
| 4 | 800      | 40          | 223    | 56.72           |

* 100% of HTTPotion failures were exceptions `(HTTPotion.HTTPError) retry_later`,
apparently thrown by [ibrowse][ibrowse], and it is harder to handle.


Then I changed to [HTTPoison][httpoison] and got a much better result.

### HTTPoison 0.8.2

| # | requests | concurrency | failed | requests/second |
|---|---|---|---|---|
| 1 | 2000     | 400         | 6      | 124.66          |

* The 6 errors were `{:error, %HTTPoison.Error{id: nil, reason: :closed}}`.

I repeated the process many times with both libraries and didn't get expressive
differences.

It is only a hobby application hosted on [heroku][heroku] free.

*I received a feedback on Slack group that I can change HTTPotion default
settings to improve number of connections, max queue per connection, etc.
I will check it and add the numbers here.*

# UPDATE

I changed [ibrowse][] configuration for [HTTPotion][] and the result is impressive!

{% highlight elixir %}
response = HTTPotion.post "http://example.com", [
  ibrowse: [max_sessions: 100, max_pipeline_size: 10]]
{% endhighlight %}

| # | requests | concurrency | failed | requests/second |
|---|---|---|---|---|
| 1 | 4000     | 4000        | 18     | 67.03           |
| 2 | 4000     | 3500        | 7      | 63.80           |
| 3 | 4000     | 2500        | 5      | 77.54           |
| 4 | 4000     | 1500        | 8      | 72.53           |
| 5 | 4000     | 1000        | 4      | 71.98           |
| 6 | 3000     | 600         | 4      | 69.17           |
| 7 | 2000     | 400         | 6      | 62.95           |

Since I got a much better result using this configuration, I used the same values
for requests and concurrency as in #1 using [HTTPoison][], and the results are
similar.

Most of the failures are related to `SSL handshake failed (5)` which looks like
is something internal to heroku.

Now I am curious to compare heroku dynos 2x vs 1x and improvements on database.
I may do it in a future post.


[heroku]: https://www.heroku.com
[httpoison]: https://github.com/edgurgel/httpoison
[httpotion]: https://github.com/myfreeweb/httpotion
[ibrowse]: https://github.com/myfreeweb/httpotion
[phoenix]: http://www.phoenixframework.org
