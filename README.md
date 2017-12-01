<div align="center">
<h1>named-urls</h1>

Simple named url patterns in Javascript
</div>

<hr />

[![Join the chat at https://gitter.im/tricoder42/named-urls](https://badges.gitter.im/tricoder42/named-urls.svg)](https://gitter.im/tricoder42/named-urls?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![CircleCI][Badge-CI]][CI]
[![Code Coverage][Badge-Coverage]][Coverage]
[![PRs Welcome][Badge-PRWelcome]][PRWelcome]
[![MIT License][Badge-License]][LICENSE]

[![Watch on GitHub][Badge-Watch]][Watch]
[![Star on GitHub][Badge-Stars]][Star]
[![Tweet][Badge-Twitter]][Twitter]

## Installation

```
yarn add named-urls
```

## Quickstart

Create file with all routes in your application (e.g. `routes.js`). Use
`named-urls/include` to create namespaced group of routes with common prefix:

```
// routes.js
import { include } from 'named-urls'

export default {
   // simple route
   profile: '/profile',
   
   // Routes with common path prefix
   auth: include('/auth', {
      // Absolute url (ignore /auth prefix)
      login: '/login/',
      
      // Relative urls (prefixed with /auth)
      passwordReset: 'password/reset/',
      passwordVerify: 'password/verify/',
   }),
   
   // Routes with params
   messages: include('/messages', {
      all: '',
      
      detail: ':messageId/',
      edit: ':messageId/edit/',
      comments: ':messageId/comments/',
   })
}
```

Use routes in `Route` component from `react-router-dom`:

```jsx
// App.js

import * as React from 'react'
import { Switch, Route } from 'react-router-dom'

import routes from './routes'
import * as scenes from './scenes'

function App() {
   return (
      <Switch>
         <Route path={routes.profile} component={scenes.Profile />
         <Route path={routes.auth.login} component={scenes.auth.Login />
         // ...
         <Route path={routes.messages.detail} component={scenes.messages.Detail />
      </Switch>
   )
}
```

Routes with parameters can be formatted using `reverse` function:

```jsx
// Navigation.js
import * as React from 'react'
import { Link } from 'react-router'
import { reverse } form 'named-urls'

function Navigation({ messages }) {
   return (
      <ul>
         <li><Link to={routes.profile}>Profile</Link></li>
         // ...
         // Use reverse to replace params in route pattern with values
         {messages.map(message => 
            <li key={message.id}>
               <Link to={reverse(routes.messages.detail, { messageId: message.id })}>
                  Profile
               </Link>
            </li>
         )}
      </ul>
   )
}
```

## License

[MIT][License]

[Badge-CI]: https://img.shields.io/circleci/project/github/tricoder42/named-urls/master.svg
[Badge-Coverage]: https://img.shields.io/codecov/c/github/tricoder42/named-urls/master.svg
[Badge-License]: https://img.shields.io/github/license/tricoder42/named-urls.svg
[Badge-Watch]: https://img.shields.io/github/watchers/tricoder42/named-urls.svg?style=social&label=Watch
[Badge-Stars]: https://img.shields.io/github/stars/tricoder42/named-urls.svg?style=social&label=Stars
[Badge-Twitter]: https://img.shields.io/twitter/url/https/github.com/tricoder42/named-urls.svg?style=social
[Badge-PRWelcome]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square

[CI]: https://circleci.com/gh/tricoder42/named-urls/tree/master
[Coverage]: https://codecov.io/gh/tricoder42/named-urls
[License]: https://github.com/tricoder42/named-urls/blob/master/LICENSE
[Watch]: https://github.com/tricoder42/named-urls/watchers
[Star]: https://github.com/tricoder42/named-urls/stargazers
[Twitter]: https://twitter.com/intent/tweet?text=Check%20out%20named-urls!%20https://github.com/tricoder42/named-urls%20%F0%9F%91%8D
[PRWelcome]: http://makeapullrequest.com
