---
layout: post
title: Window Azure Mobile Services with a Knockout View Model
date: '2013-06-23 19:55:18'
---

I have been playing around with Knockout recently and wanted a quick and simple way to save my data over a remote Ajax call, and thought Windows Azure Mobile Services (WAMS) could be a good solution. In turns out it is incredibly simple to set up a mobile service and begin posting and updating data from JavaScript (and many other supported clients), but it is worth pointing out that you can't just send your Knockout View Model along with all the extra observable information to the mobile service URL. Luckily, <a href="http://knockoutjs.com/documentation/json-data.html">Knockout supports two helper methods</a>:

ko.toJSON and ko.toJS.

In the case of WAMS, it is actually the latter you need to use, as I had trouble sending raw JSON to the insert function (presumably WAMS is expecting a POJO which it then stringifies).

The following is very simple, but complete working example:

`var DL = DL || {};
DL.app = function(window, $, undefined) {
var client = new WindowsAzure.MobileServiceClient( "[your mobile service url]", "[your app key]");
return {
  PersonViewModel: function(firstName, lastName) {
    var self = this;
    self.firstName  = ko.observable(firstName);
    self.lastName = ko.observable(lastName);
    self.save = function() {
      var js = ko.toJS(self);
      client.getTable('People').insert(js);
      console.log('saved');
    }
  };
}(window, jQuery);
ko.applyBindings(new DL.app.PersonViewModel("",""));`
