---
layout: post
title: "Timezone for RSpec tests"
comments: true
categories:
    ruby
    rails
    rspec
    test
    timezone
---

Don't set `Time.zone = 'Pacific Time (US & Canada)'`. It will change the Time
Zone for the rest of your tests.


Instead, you can implement a RSpec callback on that sets the timezone only for
the specific test.

{% highlight ruby %}
# spec/support/timezone.rb

config.around :example, :tz do |example|
  Time.use_zone(example.metadata[:tz]) { example.run }
end
{% endhighlight %}

Then you can simply set the `tz` metadata with the timezone you want to use on
your test.

{% highlight ruby %}
it 'displays start time with user timezone', tz: 'Pacific Time (US & Canada)' do
  user_timezone = 'Brasilia'
  start_date = Time.zone.parse('2017-12-31 23:00:00')
  event = Event.new(name: 'World Cup', start_date_time: start_date)
  name_with_start_date = event.name_with_start_date(user_timezone)

  expect(name_with_start_date).to eq 'World Cup (Jan 1, 2018)'
end
{% endhighlight %}

References:

[RSpec Documentation - metadata][RSpec-documentation]

[Using RSpec metadata (rossta)][using-rspec-metadata]


[RSpec-documentation]: https://relishapp.com/rspec/rspec-core/docs/metadata/user-defined-metadata
[using-rspec-metadata]: https://rossta.net/blog/using-rspec-metadata.html
