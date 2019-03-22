---
layout: post
title:  "react-router-dom route component requires page reload"
date:   2018-03-21 023:08:45Z
categories: react
---
When calling history.push('/packages') the url is updated but the component will not mount (render) unless the page is reloaded. If I call createHistory({forceRefresh: true}) or manually reload the page the UI is rendered correctly. How can I configure react-router-dom to load the component without explicitly reloading the page or using forceRefresh?

Create a history object and export it in index.jsx and use Router instead of BrowserRouter, passing history as a prop. History can then be imported to other components.

{% highlight js %}
// index.jsx
import 'bootstrap/dist/css/bootstrap.min.css'
import React from 'react'
import ReactDOM from 'react-dom'
import { Router } from 'react-router-dom' // change from { BrowserRouter }
import store from './store'
import {Provider} from 'react-redux'
import App from './App'
import createHistory from 'history/createBrowserHistory'

export const history = createHistory() // add

ReactDOM.render(
  <Provider store={store}>
    <Router history={history}>
      <App />
    </Router>
  </Provider>,
  document.getElementById('app')
);
{% endhighlight %}
