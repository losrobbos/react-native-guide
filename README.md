# Guide & Resources

## Sample Project

Find here a quick starter project which shows a full React native:

https://github.com/losrobbos/react-native-auth

The sample shows you:

- Screen Components (= like "Page components" in normal React apps)
- Styling using the StyleSheet component (= Native Apps do not know CSS)
- Central state management (Context)
- Authentication with JWT
- Stack navigator

You probably can see in the sample:
- a lot of React concepts still work the very same in a React native application
- also state management is practically the same (both for Context & Redux)

The main differences:
- We do not have HTML in apps. Therefore we have other default components for layouting like `<View>` or `<Text>`
- Apps do not know the concept of CSS. So we also "emulate" or fake the concept of CSS using the helper class `StyleSheet`
- Page components are typically called "Screens"
- Apps are typically not tested in the browser anymore (just for basic functionality checking)
- Browser concepts like Cookies or LocalStorage do not exist


## Differences in Authentication

In Native Apps something like cookies does not exist. Neither localStorage. 

Cookies and localstorage are Browser concepts.

But your native apps do not run in any browser. Therefore we cannot make authentication with cookies anymore. 

So where do you store the f***** tokens in the frontend?

Well, because Apps don't have page refreshes, we never lose our state (just in case we really close the f*** app). 

So we could simply put the token in state and as long as the app stays open (and the token is still valid / not expired), we will stay logged in.

But if we do not use cookies for exchanging the token anymore - how do we then receive the token from the API - and the other way round - how do we send our token to the API on each request?

There is another very common technique for exchanging tokens in the web using HTTP "headers". It is actually quite straight-forward.

Here some resources where you can check how to do Auth between Frontend & backend using headers:

Authentication without cookies from React native to API:

Backend Login => function loginUser => send token directly in body (not cookie attaching)
https://github.com/losrobbos/todo-backend/blob/master/controllers/usersController.js

Frontend - Login => store received token & user in state:
https://github.com/losrobbos/react-native-auth/blob/master/screens/Login.js

Backend Middleware => look for token not in cookies, check it in headers:
https://github.com/losrobbos/todo-backend/blob/master/middleware/authentication/authenticator.js

Frontend -> access protected routes - put token in request header:
https://github.com/losrobbos/react-native-auth/blob/master/contexts/apiCalls.js



## Navigation concepts

Navigation in React native has a bit more variants than traditional "react-router-dom" routing..

React Navigation concepts - Intro:
https://www.youtube.com/watch?v=OmQCU-3KPms&list=PL4cUxeGkcC9ixPU-QkScoRBVxtPPzVjrQ&index=19

React Navigation concepts show case + Authentication + Protecting routes:
https://www.youtube.com/watch?v=nQVCkqvU1uE



## Connect to API on localhost from the emulator

If you want to connect to an API running on localhost, doing a fetch or axios call to "localhost:5000" will not work.
Actually once your app runs on an emulator (or the phone), localhost will refer to this decive. And not to your PC anymore!
See here which address to use for connecting both:
https://stackoverflow.com/questions/6760585/accessing-localhostport-from-android-emulator