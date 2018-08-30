---
layout: post
title: "Syntax Highlight on Froala Editor using Webpacker"
comments: true
categories:
    ruby
    rails
    ckeditor
    froala
    webpacker
    webpack
---

*For this post, I used froala-editor 2.8.4 and codemirror 5.40.0.*

I started using Froela Editor recently and the experience is being really good, but having to add
the syntax highlight for the HTML Editor was a headache. Fortunatelly I found a solution to make
everything work properly using Webpacker with Ruby on Rails.

In order to enable the syntax highlight, you will need to add `codemirror` library.

First install it:
{% highlight bash %}
yarn add codemirror
{% endhighlight %}

After that, import the JavaScript and the CSS for CodeMirror:
{% highlight js %}
import CodeMirror from 'codemirror';
import 'codemirror/mode/xml/xml';

import 'codemirror/lib/codemirror.css';
{% endhighlight %}

Finally, wherever you call `$('.element').froalaEditor`, add the codeMirror option like here:
{% highlight js %}
$('.element').froalaEditor({
  codeMirror: CodeMirror
});
{% endhighlight %}

You need to add the `codeMirror` option because by default, Froala Editor tryies to use
`window.CodeMirror`, but as we just imported it, CodeMirror is not available on `window`.
Instead of setting codeMirror option, you could set `window.CodeMirror = CodeMirror`,
but it is not a clean solution.

In the end, the code should look like this:

{% highlight js %}
import CodeMirror from 'codemirror';
import 'codemirror/mode/xml/xml';
import 'froala-editor/js/froala_editor.pkgd.min';

import 'codemirror/lib/codemirror.css';
import 'froala-editor/css/froala_editor.pkgd.css';

document.addEventListener('turbolinks:load', () => {
  $('.element').froalaEditor({
    codeMirror: CodeMirror
  });
});
{% endhighlight %}