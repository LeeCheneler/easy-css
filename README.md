# easy-css
![Travis CI build status](https://travis-ci.org/LeeCheneler/easy-css.svg?branch=master)
![Latest npmjs version](https://badge.fury.io/js/easy-css.svg)

easy-css is a simple, layout only ITCSS and BEMIT SASS framework. It does not extend beyond the object layer in ITCSS and so has no visual styling.

#### Demo
[https://leecheneler.github.io/easy-css/demo/](https://leecheneler.github.io/easy-css/demo/)

## Getting Started

easy-css is designed to be extended, not consumed. If you just compiled and used it in your site you will find that you hit specificity issues when placing your own CSS beneath it.

#### Install easy-css
```
npm install easy-css --save
```

#### Setup ITCSS Folders
You need to set up your own ITCSS architecture within your app. Then import each layer of easy-css into each of your layers one by one to serve as the bedrock of you ITCSS project.

##### src/sass/_base.scss
```
@import 'easy-css/base';
```

##### src/sass/_objects.scss
```
@import 'easy-css/objects';
```

##### src/sass/_resets.scss
```
@import 'easy-css/resets';
```

##### src/sass/_settings.scss
```
@import 'easy-css/settings';
```

##### src/sass/_tools.scss
```
@import 'easy-css/tools';
```

##### src/sass/_utilities.scss
```
@import 'easy-css/utilities';
```

##### src/sass/main.scss
```
@import 'settings';
@import 'tools';
@import 'resets';
@import 'base';
@import 'objects';
@import 'utilities';
```

#### Compiling You SASS
This library won't have widespread use so I'm going to assume you're familiar with webpack and how to load CSS via it. (I recommend css-loader/postcss-loader/sass-loader).

Here is some example config to configure webpack:
```
{
  // Load .scss and .css files through the following loaders:
    // - sass-loader (compiles sass to css)
    // - postcss-loader (applies autoprefixer plugin to css)
    // - css-loader
    // - loads css as plain text
  // Then the ExtractTextPlugin swallows the output and injects it as a css file on the web page
  test: /\.s?css$/,
  use: ExtractTextPlugin.extract({
    fallback: 'style-loader',
    use: [
      {
        loader: 'css-loader'
      },
      {
        loader: 'postcss-loader',
        options: {
          plugins: () => [
            autoprefixer({
              browsers: ['last 2 versions', 'ie 9-11']
            })
          ]
        }
      },
      {
        loader: 'sass-loader',
        options: {
          includePaths: [
            path.resolve(__dirname, './node_modules/easy-css')
          ]
        }
      }
    ]
  })
},
```

## Inspiration
Great inspiration was taken from the [nebula-css](https://github.com/rbrtsmith/nebula-css) framework written by a great CSS author Robert Smith. He's been a great mentor throughout its development.
