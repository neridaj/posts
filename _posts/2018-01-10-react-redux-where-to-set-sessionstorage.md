---
layout: default
title:  "React/Redux where to set sessionStorage"
date:   2019-01-10 01:10:05Z
categories: react
---
If using react with redux to manage state, where should sessionStorage items be set? There doesn't appear to be any hard-and-fast rules regarding this but if sessionStorage is just treated as another store then the reducer is probably a good option.

{% highlight js %}
// actions/loginActions.js
export function loginUser(user) {
  return function(dispatch) {
    return LoginApi.login(user).then(creds => {
      dispatch(loginUserSuccess(creds));
    }).catch(error => {
      throw(error);
    });
  };
}
export function loginUserSuccess(creds) {
  return {
    type: types.LOGIN_USER_SUCCESS,
    state: creds
  }
}
// reducers/loginReducer.js
export default function loginReducer(state = Map(), action) {
  switch (action.type) {
    case types.LOGIN_USER_SUCCESS:
      sessionStorage.setItem('credentials', JSON.stringify(action.state))
      return state.set('credentials', action.state);
    default:
      return state;
  }
}
{% endhighlight %}
