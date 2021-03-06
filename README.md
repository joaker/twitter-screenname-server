# Twitter Compose

## Demo

Check out the demo [here](https://tweetify-composer.herokuapp.com/)

Note: The first request to heroku after a while of activity takes between 2 and 10 seconds to complete.  Subsequent requests will be quicker

## Description

Compose a tweet with auto-complete for screen names (e.g.: @davidd => @daviddavidson)

This user interface is written in React and Redux, in ES2015 transpiled by babel.  The components are stateless (the one class-y component is a PureComponent), and actions are generated by action creators.  redux-thunk allows for convenient action creator composition through nested dispatches.

## Webpack Shennanigans

- The Provide Plugin is defining React, ReactDOM, and the classnames module
- The Alias Plugin basically registers important regions as modules, so they are be easily referenced with "../..etc../.."
- The hot module replacement on the `npm run dev` task does not work quite right for components.  Styles are fine, though
- Tranpilation of jsx and javsacript is delegated by Webpack to Babel

## Features

- **Compose with screen name suggestions**  
The UI starts suggesting screen names fetched from Twitter after the second screen name character (not including the @ character)

- **Debounced screen name resolution**
Each change to the partial screen name triggers a request to resolve associated screen names.  These requests are debounced to provide a smoother UI experience and to limit bandwidth consumption.  One request is sent each time there is a break in rapid typing

- **Keyboard Navigation**
  - Normal Mode (when suggestions ARE NOT displayed):
    - Enter: Submit the current tweet (replace current token)
    - Down: normal input behavior
    - Up: normal input behavior
    - Escape: close suggestion list
  - Context Assist Mode (when suggestions ARE displayed):
    - Enter: Accept current suggestion (replace current token)
    - Down: Select next suggestion
    - Up: Select previous suggestion
    - Escape: Close the suggestions

##Usage

Clone the repo
`npm clone https://github.com/joaker/twitter-screenname-server`

Install the npm modules
`npm i`

Start the service
`npm run`

## Server setup

This was tested using Node v6.2.2, but any minor version of Node v6 should work.

Use `npm install` to install all dependencies.

Use `npm run start` to start the Twitter lookup server

Navigate to [http://localhost:3001/](http://localhost:3001/) to ensure the local server is responding to requests. If the URL loads, attempt to make a sample user search request http://localhost:3001/twitter/user/search?username=chicago
