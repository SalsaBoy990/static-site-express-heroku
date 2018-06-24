---
title: "Welcome to static-site-express"
date: "2018-06-22"
excerpt: "static-site-express is a simple Node.js based static site generator that uses EJS and Markdown."
cover: "./assets/images/blackhole.jpg"
comments: false
topic: null
---

static-site-express is a simple Node.js based static site generator that uses EJS and Markdown.


## Usage Manual

### 1. Installation


`npm install static-site-express`


### 2. Generate website into `./public` folder

Build website only (without serving it on localhost):

`npm run build`

Build website, watch changes (fs changes in `./src` folder trigger re-build) and serve it at `localhost:4000`:

`npm run build-watch`

Inspect `site.config.js` first. You can change the site properties (title, author, description, social media links etc.) that are used in the EJS partials. The site generator will insert your values into the right place.

The `./lib` folder contains the JS files used for building and serving the website.


### 3. Register at Netlify and publish your website

Register [here](https://www.netlify.com/){.underline}, and [see this tutorial video](https://www.netlify.com/docs/continuous-deployment/){.underline}.

Build command is: `npm run build`

Publish directory is: `public`

The `netlify.toml` configuration file already contains these two settings. You can publish your site in a minute.

### +1. You can even publish the website on Heroku!

A `Procfile` already supplied for you with the command  to execute the app server by the dynos:

`web: node ./heroku/serve.js`

The Express server will run on Heroku, but you need improve security!
(For serving on localhost there is no need for this). For example, you really should set security headers with the `helmet` npm package:

````javascript
// Set Security Headers.
const helmet = require('helmet')

app.use(helmet())
````

You can also set CSP rules:

````javascript
// Content Security Policy.
const csp = require('helmet-csp')

// An example, with some exeptions:
app.use(csp({
  directives: {
    defaultSrc: [`'self'`],
    styleSrc: [`'self'`, 'https://fonts.googleapis.com', 'https://www.youtube.com'],
    fontSrc: [`'self'`, 'https://fonts.gstatic.com/'],
    scriptSrc: [`'self'`, 'https://www.youtube.com','https://www.googletagmanager.com', 'https://www.google-analytics.com'],
    childSrc: [`'self'`, 'https://www.youtube.com'],
    imgSrc: [`'self'`, 'www.google-analytics.com'],
    objectSrc: [`'self'`],
    connectSrc: [`'self'`]
  }
}))
````

You have to build the site in the `public/` folder first. Change the `.gitignore` rules too!


## The idea of making a static site generator came from this article:

* Douglas Matoso 2017. [Build a static site generator in 40 lines with Node.js](https://medium.com/douglas-matoso-english/build-static-site-generator-nodejs-8969ebe34b22){.underline}. 


## Future tasks

* Use paginator on the index page


## Q&A

If you have a question ask me: [guland@protonmail.com](mailto:guland@protonmail.com){.underline}, or [open an issue here](https://github.com/SalsaBoy990/static-site-express/issues){.underline}.