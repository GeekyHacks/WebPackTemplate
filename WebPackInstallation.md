# WebPack

- If you gonna create any project using webpack try to install it first into your package before any other dependencies to test it and see if its working fine because it will be the base of your whole project structure, this summary will have a link of webpack  template that you can use when creating your repo
- the beauty of webpack is that it helps you bundle your project easily using JS code only, so you might not need to use css anymore
- it help you run your project in your own server with instance reload
- create `src` folder and create an `index.js` file to import all your js code to it, basically webpack will start from this file, its called `main` in your package.json file and its path is mentioned in there
- use `npm init -y` to create your package file automatically
- use `npm i -D webpack webpack-cli` to install the package in your dependencies section
- create a file `webpack.config.js` in your main folder to start configuring your webpack
- start by putting the following code

```jsx
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const BundleAnalyzerPlugin =
  require('webpack-bundle-analyzer').BundleAnalyzerPlugin

module.exports = {
  mode: 'development',
  entry: {
// __dirname will start in the current directory 
    bundle: path.resolve(__dirname, 'src/index.js'),
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name][contenthash].js',
    clean: true,
    assetModuleFilename: '[name][ext]',
  },
  devtool: 'source-map',
  devServer: {
    static: {

      directory: path.resolve(__dirname, 'dist'),
    },
    port: 3000,
    open: true,
    hot: true,
    compress: true,
    historyApiFallback: true,
  },
  module: {
    rules: [
      {
        test: /\.sass$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
      {
//bable loader will make your project functional on all browsers 
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
//this will load all images
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: 'asset/resource',
      },
    ],
  },
//this will build the dist html file based on the template file
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Webpack App',
      filename: 'index.html',
      template: 'src/template.html',
    }),
// this plugin will show you a visual layout of what your 
//bundle looks like
    // new BundleAnalyzerPlugin(),
  ],
}
```

- install sass `npm i -D sass style-loader css-loader sass-loader`
- install `npm i -D html-webpack-plugin` so you can generate an html file using webpack
- make sure you have the following package.json code

```json
{//this part is created by npm init -y
  "name": "webpack-starter",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
// this part you have to input it so you can run them
  "scripts": {
    "build": "webpack",
    "start": "webpack serve"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
//devdeps are essinctal to make you code run perffectly
//you can add more deps here just by using the npm install(or i -D) + the package name
    "@babel/core": "^7.17.8",
    "@babel/preset-env": "^7.16.11",
    "babel-loader": "^8.2.3",
    "css-loader": "^6.7.1",
    "html-webpack-plugin": "^5.5.0",
    "sass": "^1.49.9",
    "sass-loader": "^12.6.0",
    "style-loader": "^3.3.1",
    "webpack": "^5.70.0",
    // "webpack-bundle-analyzer": "^4.5.0",
    "webpack-cli": "^4.9.2",
    "webpack-dev-server": "^4.7.4"
  },
  "dependencies": {
//here are the dep you gonna use in your code 
  //  "axios": "^0.26.1"
  }
}
```

- `npm i -D babel-loader @babel/core @babel/preset-env` to install babel that will make your code run on browsers
- build  your bundle `npm run build`
- to liveview your code `npm run dev`
-