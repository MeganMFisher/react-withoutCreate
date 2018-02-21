npm init

* React and React-DOM are the core modules needed to start.

npm install --save react react-dom


* Use React with Babel so you can use ES6 and JSX in your JavaScript code.

npm install --save-dev babel-cli babel-preset-react babel-preset-es2015 babel-loader


* Create a Babel configuration file by running

echo '{ "presets": ["react", "es2015"] }' > .babelrc


* You will need webpack and webpack-dev-server

npm install --save-dev webpack webpack-dev-server


* Configure webpack to run using webpack-dev-server locally

touch webpack.config.js

* Add the following into webpack.config.js

var webpack = require('webpack')
var path = require('path')
module.exports = {
  entry: path.resolve(__dirname, 'app'),
  output: {
    path: __dirname + '/dist',
    publicPath: '/',
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: path.resolve(__dirname, 'public')
  },
  module: {
    loaders: [
      {test: /\.js$/, exclude: /node_modules/, loaders: ['babel-loader']},
      {test: /(\.css)$/, loaders: ['style-loader', 'css-loader']}
    ]
  }
}

* We need to include path, css-loader and style-loader modules since they are being used.

npm install --save-dev path style-loader css-loader


* Create public and component directories and also the index.html file which will contain a skeletal html structure. 

mkdir components public && touch public/index.html index.js
 

* Create your main componement

touch App.js


* Add the following to your App.js
 
import React, {Component} from 'react';

class App extends Component() {
    render() {
        return (
          <div>
            <h1>Hello World</h1>
          </div>
        )
    }
}
export default App;


* Add the following to your index.html

<!DOCTYPE html>
<html>
  <head>
    <title>Simplest React App Setup</title>
  </head>
  <body>
    <div id='app'></div>
    <script src='/bundle.js'></script>
  </body>
</html>


* Add the following to your index.js

import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'
ReactDOM.render(<App />, document.getElementById('app'))


* Add the following to your scripts in your package.json

"start": "webpack-dev-server"


* You are ready to go!

npm start