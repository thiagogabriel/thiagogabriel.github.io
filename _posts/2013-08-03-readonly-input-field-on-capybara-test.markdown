---
layout: post
title: "Readonly input field on capybara test"
date: 2013-08-03 15:51
comments: true
categories: 
    development
    capybara
    rails
    pickadate
---

This week it was decided to replace all date fields in the project with [pickadate.js][]. It was a smooth change using [pickadate-rails][] gem. Using simple_form, you have to change the input to something like this 

```erb app/views/users/_form.html.erb
{% highlight ruby %}
<%= f.input :birthday, as: :string, input_html: { class: "datepicker" } %>
{% endhighlight %}
and the application.js can be something like this

javascript app/assets/javascripts/application.js
{% highlight ruby %}
('.datepicker').pickadate({
    format: 'yyyy-mm-dd',
    selectYears: true,
    selectMonths: true
});
{% endhighlight %}

<!--more-->

Then it started a problem on capybara tests, because birthday is a mandatory field and the input becames readonly because of the [pickadate.js][] plugin.

Searching into capybara API, I didn't find something like `fill_in 'Birthday', :with => '1990-08-24', force: true`, so the solution I got is to hack [executing some javascript][capybara-scripting] in the page context.

ruby spec/acceptance/user_form_spec.rb
{% highlight ruby %}
describe "Create user", :js => true do
  it {
    visit '/users/new'
    fill_in :name, with: 'Batman'
    page.execute_script("$('#datepicker').removeAttr('readonly')")
    fill_in :birthday, with: '1970-01-01'
    find_button('Save').trigger('click')
    page.should have_content('User was successfully created.')
  }
end
{% endhighlight %}

Line 5 removes readonly attribute from input and line 7 is also very important if you are testing [pickadate.js][], because when you fill birthday, it pops up a box which blocks the click on 'Save'. Using this `trigger('click')`, capybara ignores the box in front, and you can click on save.

![image](/images/posts/2013-08-03/pickadate-popup.jpg)

An easier solution is to set the field value directly through javascript:
```javascript
page.execute_script("$('#datepicker').val('1970-01-01')")
```
On this way you don't need to use `trigger('click')`.


[pickadate.js]: http://amsul.ca/pickadate.js
[pickadate-rails]: https://github.com/veracross/pickadate-rails
[capybara-scripting]: http://rubydoc.info/github/jnicklas/capybara/master#Scripting
