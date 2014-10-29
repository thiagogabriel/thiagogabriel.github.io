---
layout: post
title: "Manage Objective-C dependencies with Cocoapods on Swift project"
comments: true
categories:
    swift
    cocoapods
    xcode
    apple
---

One of my biggest concerns when Apple announced Swift lang was how to
integrate Objective-C libraries on new projects. I'm not a big fan of
Objective-C, but there are many awesome libraries on [Cocoapods][cocoapods]
like [AFNetworking][afnetworking] for networking activities like HTTP
requests and [MBProgressHUD][mbprogresshud] for activity indication,
like "loading" or "completed" notification. They are almost essential
for most of iOS apps and Cocoapods is the best way to manage dependencies
for Objective-C code.

Fortunately Apple documented the process to use Objective-C code on Swift
projects and I'll cover it step by step.

## 1. Install Cocoapods

It is quite simple. Just open your terminal and run
`sudo gem install cocoapods`.

## 2. Initialize cocoapods

On your iOS project, type `pod init`. It generates Podfile with the
content below.

{% highlight ruby linenos %}
# Uncomment this line to define a global platform for your project
# platform :ios, "6.0"
source 'https://github.com/CocoaPods/Specs.git'

target 'CocoapodsExample' do

end

target 'CocoapodsExampleTests' do

end
{% endhighlight %}

## 3. Add the dependencies on Podfile

Podfile should have all the dependencies you need on your project.
Now you add the dependencies inside the target block:

{% highlight ruby %}
...
target 'CocoapodsExample' do
  pod 'MBProgressHUD', '~> 0.9'
end
...
{% endhighlight %}

## 4. Install the dependencies

`pod install`

## 5. Open you project with YourApp.xcworkspace

From now on, you *always* open you project using `.xcworkspace` file.

## 6. Add a Bridging Header for Objective-C libraries

Create a Header file on you project.

![New header 1](/images/posts/2014-10-29/new-header-file-1.png)

![New header 2](/images/posts/2014-10-29/new-header-file-2.png)

On the header file, import the library you added via Cocoapods or any other Objective-C library you would like to use on your Swift App.

{% highlight objective-c %}
//
//  Pods-Bridging-Header.h
//  CocoapodsExample

#import "MBProgressHUD.h"
{% endhighlight %}

Add Objective-C Bridging Header on build settings. The path should be relative to your project.

![Bridging header](/images/posts/2014-10-29/bridging-header.png)


## 7. Enjoy

If you followed the steps correctly it should be working. You don't need to import the headers. It is already imported on `Pods-Bridging-Header.h`.

![Bridging header](/images/posts/2014-10-29/works.png)





[cocoapods]: http://cocoapods.org/
[afnetworking]: https://github.com/AFNetworking/AFNetworking
[mbprogresshud]: https://github.com/jdg/MBProgressHUD
