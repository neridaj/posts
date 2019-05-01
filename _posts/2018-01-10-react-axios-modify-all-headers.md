---
layout: default
title:  "React config default request headers"
date:   2019-01-10 20:11:12Z
categories: react
---
Setting default headers for all requests is pretty straightforward with axios. Not so much with fetch-intercept.

{% highlight js %}
// api/config.js
import axios from 'axios';

axios.defaults.headers.common['My-Header'] = 'IsBetterThanYours';

const axiosInstance = axios.create();
axiosInstance.interceptors.request.use(
  config => {
    sessionStorage.getItem('credentials') ? config.headers['Authorization'] = 'Bearer ' + JSON.parse(sessionStorage.credentials).authToken : undefined;
    return config;
  },
  error => Promise.reject(error)
);

export default axiosInstance;
{% endhighlight %}
