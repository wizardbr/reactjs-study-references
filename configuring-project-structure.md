## Configure a reactjs project structure

<p>First of all create a new nodejs application:</p>

- `yarn init -y`

<p>We need to add the following libs to create the configuration for development environment:</p>

- `yarn add @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli -D`

<p>Noew we need to install react and react-dom:</p>

- `yarn add react react-dom`

### Babel configuration

<p>We need to create the babel.config.js and set the preset conf:</p>

```js
module.exports = {
  presets: ["@babel/preset-env", "@babel/preset-react"]
};
```

<p>Now we should create a src folder with index.js entry.</p>

<p>Now we should create a public folder.</p>

<p>create webpack.config.js</p>

```js
const path = require("path");

module.exports = {
  entry: path.resolve(__dirname, "src", "index.js"),
  output: {
    path: path.resolve(__dirname, "public"),
    filename: "bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
```

<p>To handle js files in transpilation we need to add the following lib:</p>

- `yarn add babel-loader -D`

<p>Now in your package.json you need to create the following script:</p>

```json
"scripts": {
    "build": "webpack --mode development"
  },
```

### Configuring hot reload

<p>We need to install the following lib:</p>

- `yarn add webpack-dev-server -D`

<p>In your webpack.config.js you need to add the following configuration:</p>

```js
devServer: {
    contentBase: path.resolve(__dirname, 'public')
},
```

<p>And in your package.json you add the following new script:</p>

```json
  "dev": "webpack-dev-server --mode development"
```

### Configuring loader for styles

- `yarn add style-loader css-loader -D`

<p>In the module configuration you need to add a new rule, follow the example below:</p>

```js
{
  test: /\.css$/,
  use: [{ loader: "style-loader" }, { loader: "css-loader" }]
}
```

<p>In your App.js file you can import an css file and test it</p>

```js
import "./App.css";
```

### Configuring loader for images

- `yarn add file-loader -D`

<p>webpack.config.js - In the module configuration you need to add a new rule, follow the example below:</p>

```js
{
  test: /.*\.(gif|png|jpe?g)$/i,
  use: {
    loader: 'file-loader'
  }
}
```

<p>Now you can import one image in your App.js file and test it.</p>

```js
import image from './assets/image.jpg'
```

```jsx
return <img src={image} />
```
