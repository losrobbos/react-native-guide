# Guide & Resources

## Getting into React native

Official getting started guide with overview of React native concepts:
https://reactnative.dev/docs/getting-started

In order to get the big picture of React native, I recommend this very clear, free video series from the Net Ninja:

https://www.youtube.com/watch?v=ur6I5m2nTvk&list=PL4cUxeGkcC9ixPU-QkScoRBVxtPPzVjrQ

The series consists of short & straight-to-the-point mini-tutorials, demonstrating each fundamental React Native concept.

It will help you to get your initial setup, all necessary tools for developing and understanding the basic concepts before starting your app development journey.

Important key concepts to get into before start coding:
- Expo vs React Native
- Smartphone Emulator (Android & iOS)
- The Expo App
- Screen Components
- Stack Navigator
- The Stylehsheet class

## Experimenting online with "Snack"

"Expo Snack" is a webpage similar to code sandbox, where you can experiment with React Native snippets & see the result immediately live: https://snack.expo.io/

Expo Snack is very useful to get familiar with basic React native components, styling, state management & navigation, without having to setup a full project first.

## Sample Project

Find here a quick starter project which shows a full React native app: 

https://github.com/losrobbos/react-native-auth

The sample shows you:

- Screen Components (= like "Page components" in normal React apps)
- Styling using the StyleSheet class (= Native Apps do not know CSS)
- Central state management (Context)
- Authentication with JWT
- Stack navigator

You probably can see in the sample:
- a lot of React concepts still work the very same in a React native application
- also state management is practically the same (both for Context & Redux)

The main differences:
- We do not have HTML in apps. Therefore we have other default components for layouting like `<View>` or `<Text>`
- Apps do not know the concept of CSS. So we also "emulate" or fake the concept of CSS using the helper class `StyleSheet`
- Even though we can emulate CSS properties with the Stylesheet class, you need to note that there is no INHERITANCE of CSS styles to children! 
- Page components are typically called "Screens"
- Apps are typically not tested in the browser anymore (just for basic functionality checking). Instead we use the Expo App or Smartphone Emulators
- Browser concepts like Cookies or LocalStorage do not exist. So we need to store data differently on a phone compared to a browser app


## Navigation concepts

Navigation in React native has a bit more variants than traditional "react-router-dom" routing..

Instead of the famous React-Router-Dom library typically the library "React Navigation" is applied:
https://reactnavigation.org/docs/getting-started/

React Navigation concepts - Intro: 
https://www.youtube.com/watch?v=OmQCU-3KPms&list=PL4cUxeGkcC9ixPU-QkScoRBVxtPPzVjrQ&index=19

### React Navigation V5

Following walkthroughs for the React Navigation V5 concepts

Navigation with the Stack Navigator:
https://www.youtube.com/watch?v=9K7JCQbOHVA

All navigation concepts (Stack, Drawer, Tabs) - show case - with Authentication / Protecting screens:
https://www.youtube.com/watch?v=nQVCkqvU1uE

Navigation with Tabs - Deep Dive Tutorial: https://www.youtube.com/watch?v=Hln37dE19bs


## Connect to API on localhost from the emulator

If you want to connect to an API running on localhost, doing a fetch or axios call to "localhost:5000" will not work.

Actually once your app runs on an emulator (or the phone), localhost will refer to this decive. And not to your PC anymore!

See here which address to use for connecting both:
https://stackoverflow.com/questions/6760585/accessing-localhostport-from-android-emulator

So in summary: 
- address for usage in Android or iOS emulator: try addresses http://10.0.2.2:5000 or http://0.0.0.0:5000 for connecting, instead of http://localhost:5000
- address for usage in Expo app - retrieve dynamically: https://stackoverflow.com/questions/47417766/calling-locally-hosted-server-from-expo-app

## Authentication between Native App & API

In Native Apps something like cookies does not exist. Neither localStorage. 

Cookies and localStorage are Browser concepts.

But your native apps do not run in any browser. Therefore we cannot make authentication with cookies anymore. 

So where do you store the f***** tokens in the frontend?

Well, first of all, why do we actually needed to store tokens in the browser (e.g. in cookies or localstorage)?

Mainly to preserve the token info on page refreshes. Because page refreshes clear our app state every time. And if we would store tokens in state only, we would lose the information and would need to login again after each page refresh.

Now, some good news... Apps don't have page refreshes. We never lose our state (just in case we really close the app). 

So a simple solution would be to simply put the token in state. And that's it.

As long as the app stays open (and the token is still valid / not expired), we will stay logged in.

But if we do not use cookies for exchanging the token anymore - how do we then receive the token from the API - and the other way round - how do we send our token to the API on each request?

There is another very common technique for exchanging tokens in the web using "HTTP headers". It is actually quite straight-forward.

Following some resources where you can check how to do Auth between Frontend & API using headers.

### Authentication using headers

Backend Login => function loginUser => send token directly in BODY (no cookie attaching):
https://github.com/losrobbos/todo-backend/blob/master/controllers/usersController.js

Frontend - Login => store received token & user in state:
https://github.com/losrobbos/react-native-auth/blob/master/screens/Login.js

Backend Middleware => look for token not in cookies, check it in headers:
https://github.com/losrobbos/todo-backend/blob/master/middleware/authentication/authenticator.js

Frontend -> access protected routes - put token in request header:
https://github.com/losrobbos/react-native-auth/blob/master/contexts/apiCalls.js


### Keep user logged in after app closing & reopening

If you wanna keep a user logged in, even after closing the app, you need to store the token somewhere on the phone.

Therefore you can use a similar concept to localStorage from browser, the "asyncStorage":

https://docs.expo.io/versions/latest/sdk/async-storage/

