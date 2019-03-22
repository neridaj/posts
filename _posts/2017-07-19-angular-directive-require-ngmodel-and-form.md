---
layout: post
title:  "Angular 1.x accessing form and model within directive"
date:   2017-07-19 23:57:44Z
categories: angular
---
Accessing the form and controller within the linking function of a directive is achieved by passing an array to the require property. This results in an array of controllers as the fourth argument in the link function.

{% highlight js %}
angular.module('myApp')
.directive('passwordValidation', passwordValidation)
function passwordValidation(){
  return {
    replace: true,
    require: ['ngModel','^form'], // also 'form^' ?
    scope: {
      userName: '@'
    },
    link: function(scope, elem, attr, controllers) {
      var ngModelCtrl = controllers[0],formCtrl = controllers[1];
      ...
    }
  }
}
{% endhighlight %}
