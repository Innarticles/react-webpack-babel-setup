
`npm i webpack --save-dev`
`npm i webpack-cli --save-dev`

Next up add the webpackcommand inside package.json:
```
"scripts": {
  "build": "webpack --mode production"
}
```



## 2.  Babel
React components are mostly written in JavaScript ES6. ES6 is a nice improvement over the language but older browsers cannot understand the new syntax. Take the class keyword for example. Stateful React components are declared as classes (I guess it will be no longer the case sooner or later). So for getting ES6 to work in older browser we need some kind of transformation.

And that transformation is called transpiling. Webpack doesn’t know how to transform ES6 JavaScript to ES5 but it has this concept of loaders: think of them as of transformers. A webpack loader takes something as the input and produces something else as the output.

babel-loader is the Webpack loader responsible for taking in the ES6 code and making it understandable by the browser of choice.
Obsviusly babel-loader makes use of Babel. And Babel must be configured to use a bunch of presets: `npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev`

Don’t forget to configure Babel! Create a new file named .babelrc inside the project folder:
```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

## 3 How to set up React, webpack, and Babel: setting up Babel
React components are mostly written in JavaScript ES6. ES6 is a nice improvement over the language but older browsers cannot understand the new syntax. Take the class keyword for example. Stateful React components are declared as classes (I guess it will be no longer the case sooner or later). So for getting ES6 to work in older browser we need some kind of transformation.

And that transformation is called transpiling. Webpack doesn’t know how to transform ES6 JavaScript to ES5 but it has this concept of loaders: think of them as of transformers. A webpack loader takes something as the input and produces something else as the output.

babel-loader is the Webpack loader responsible for taking in the ES6 code and making it understandable by the browser of choice.

Obsviusly babel-loader makes use of Babel. And Babel must be configured to use a bunch of presets:

babel preset env for compiling Javascript ES6 code down to ES5 (please note that babel-preset-es2015 is now deprecated)
babel preset react for compiling JSX and other stuff down to Javascript
Let’s pull in the dependencies with:

npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
Don’t forget to configure Babel! Create a new file named .babelrc inside the project folder:

```
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

At this point we’re ready to define a minimal webpack configuration.
Create a file named webpack.config.js and fill it like the following:

```
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};

```


## 4. How to set up React, webpack, and Babel: writing React components
Let’s start with the right foot: we’ll create two React components following the Container / Presentational principle.

I suggest taking a look at container components and smart and dumb components by Dan Abramov for learning more. In brief, the Container / Presentational principle is a pattern for React components. The container component is the one that carries all the logic: functions for handling state changes, internal component state and so on.

In contrast a presentational component is merely used for displaying the intended markup. Presentational components are plain JavaScript functions receiving data from the container component as props.

You’ll see how they look like in the following example.

For this post’s scope I’d like to build a super simple React form with a single text input.

`npm i react react-dom`

A question I get a lot is “should I install react and react-dom as dev dependencies or not?” It doesn’t matter for the final result. webpack will still produce a bundle with your JavaScript application. I have this bad habit of putting react and react-dom in devDependencies so you’ll find that style a lot in my tutorials.



## 5 .
Next up create a minimal directory structure for organizing the components:

`mkdir -p src/js/components/{container,presentational}`

## 6. How to set up React, webpack, and Babel: the HTML webpack plugin
To display our React form we must tell Webpack to produce an HTML page. The resulting bundle will be placed inside a script tag.

Webpacks needs two additional components for processing HTML: html-webpack-plugin and html-loader.

Add the dependencies with:

npm i html-webpack-plugin html-loader --save-dev
Then update the webpack configuration:

`npm i html-webpack-plugin html-loader --save-dev`


## 7. How to set up React, webpack, and Babel: webpack dev server
You don’t want to type npm run build every time you change a file.

It takes only 3 lines of configuration to have a development server up and running. Once configured webpack will launch your application inside a browser. Also, every time you save a file after a modification webpack wev server will automagically refresh the browser’s window.

To set up webpack dev server install the package with:

npm i webpack-dev-server --save-dev
Open up package.json to add the start script:

"scripts": {
  "start": "webpack-dev-server --open --mode development",
  "build": "webpack --mode production"
}
save and close the file.

Now, by running:

npm start