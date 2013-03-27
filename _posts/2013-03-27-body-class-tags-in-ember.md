---
layout: post
title: "Adding route specific body class tags in Ember"
comments: true
author: Brian Cardarella
twitter: bcardarella
github: bcardarella
category: ember
social: true
summary: "For design!"
published: true
---

Our [designer](http://twitter.com/cssboy) likes to use body class tags
depending upon the context of the app he is designing. We're currently
building an Ember app and this is how I got it working:

{% highlight javascript %}
Ember.Route.reopen({
  enter: function() {
    this._super();
    var cssClass = this.toCssClass();
    // you probably don't need the application class
    // to be added to the body
    if (cssClass != 'application') {
      Ember.$('body').addClass(cssClass);
    }
  },
  exit: function() {
    this._super();
    Ember.$('body').removeClass(this.toCssClass());
  },
  toCssClass: function() {
    return this.routeName.dasherize();
  }
});
{% endhighlight %}