---
author: Thiago Borges
layout: post
title: "Quick tip: iOS animation on UISearchBar"
date: 2012-09-10 23:28
comments: true
categories:
  - iOS
  - Development
  - tip
---

As we can see with successful apps, transitions, animations and minimalistic design are great approach on mobile development.

Here I’ll give some quick tips when you’re using UISearchBar on iOS.

<!--more-->

This post is about the following effects:

![image](/images/posts/2013-06-22/UISearchBar.gif)

In our case, we already have UISearchBar in our .xib and UISearchBarDelegate as protocol on @interface (.h) file.

MyOwnViewController.h
{% highlight objective-c %}
@interface MyOwnViewController : UIViewController <UISearchBarDelegate> {
{% endhighlight %}

Don’t forget to set SearchBar’s Delegate on xib. This will link the “actions” of xib with you code.

And the most important, the .m implementation:

UISearchBarDelegate has many Delegate Methods. Here we’ll be using

`searchBarTextDidBeginEditing:(UISearchBar *)searchBar` (that is called when the user touches SearchBar) and<br />
`searchBarTextDidEndEditing:(UISearchBar *)searchBar` (that is called when the user touches Cancel or Search)

The code is the following:

MyOwnViewController.m
{% highlight objective-c %}
- (void)searchBarTextDidBeginEditing:(UISearchBar *)searchBar {
    [searchBar setShowsCancelButton:YES animated:YES];
    [self.navigationController setNavigationBarHidden:YES animated:YES];
}
{% endhighlight %}

MyOwnViewController.m
{% highlight objective-c %}
- (void)searchBarTextDidEndEditing:(UISearchBar *)searchBar {
    [searchBar setShowsCancelButton:NO animated:YES];
    [self.navigationController setNavigationBarHidden:NO animated:YES];
}
{% endhighlight %}
