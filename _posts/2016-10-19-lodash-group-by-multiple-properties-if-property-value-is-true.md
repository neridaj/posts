---
layout: default
title:  "Grouping by multiple properties using lodash"
date:   2019-01-10 19:10:30Z
categories: lodash
---
Creating composite objects from an array of "selected" objects is achieved with filter and groupBy.

{% highlight js %}
// inital array of objects
[
  {
      id: 1,
      selected: true,
      makeCode: "Make-A",
      modelCode: "Model-a",
      trimCode: "trim-a",
      yearCode: "2012"
  },
  {
      id: 2,
      selected: false,
      makeCode: "Make-A",
      modelCode: "Model-a",
      trimCode: "trim-a",
      yearCode: "2013"
  },
  {
      id: 3,
      selected: true,
      makeCode: "Make-B",
      modelCode: "Model-c",
      trimCode: "trim-a",
      yearCode: "2014"
  },
  {
      id: 25,
      selected: true,
      makeCode: "Make-C",
      modelCode: "Model-b",
      trimCode: "trim-b",
      yearCode: "2012"
  },
  {
      id: 26,
      selected: true,
      makeCode: "Make-C",
      modelCode: "Model-b",
      trimCode: "trim-a",
      yearCode: "2013"
  }
]
//desired result
{
    Make-A: {
        Model-a: {
            count: 1
        }
    }
},

{
    Make-B: {
        Model-c: {
            count: 1
        }
    }
},
{
    Make-C: {
        Model-b: {
            count: 2
        }
    }
}
//steps
var selectedVehicles = _.filter(response.vehicleTypes, 'selected');
selectedVehicles = _.groupBy(selectedVehicles, function(item) {
  return item.makeCode;
});
_.forEach(selectedVehicles, function(value, key) {
  selectedVehicles[key] = _.groupBy(selectedVehicles[key], function(item) {
    return item.modelCode;
  });
});
{% endhighlight %}
