---
layout: post
title: "Freeze String Literal for Ruby on Rails"
comments: true
categories:
    ruby
    rails
    memory
    performance
---

Something that always bothered me was rubocop asking to add
`# frozen_string_literal: true` to my ruby files. I always ended up removing the
option on rubocop configuration.

{% highlight yml %}
# Don't do it, unless the memory usage doesn't matter!!!
Style/FrozenStringLiteralComment:
  Enabled: false
{% endhighlight %}

It turns out that this comment can save a lot of memory on your running
projects. This option avoids the same string being allocated many times in the
memory.

To add the magic comment to the beginning of all ruby files, simply run this
command:

{% highlight bash %}
# You must have the gem rubocop installed
bundle exec rubocop --auto-correct --only FrozenStringLiteralComment
bundle exec rubocop --auto-correct --only Layout/EmptyLineAfterMagicComment
{% endhighlight %}

The second command is to add a blank line after the magic comment. I'm not sure
how to run two rubocop `--only` at once, so I prefer to run the two commands.

The result of this was that I was receiving notifications about the high memory
usage, and after that, the project never had a memory issue again.

References:

[Freelancing Gods - Friendly Frozen String Literals][freelancing-gods]

[Pluralsight - Ruby 2.3: Working with immutable strings][pluralsight]


[freelancing-gods]: https://freelancing-gods.com/2017/07/27/friendly-frozen-string-literals.html
[pluralsight]: https://www.pluralsight.com/blog/software-development/ruby-2-3--working-with-immutable-strings-
