### A quite exhaustive React, Node, Mongo App to Create, Edit, Delete and render tabular data. Have implemented filter functionality for text-based search and date-range based search. Have used Material-UI extensively across the app.

##### Quite a few standard and simple tests have also been implemented with `jest`

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

### To launch this project in the local machine.

run `npm install` in both the `./server` and `./client` directories separately, which will install all the npm packages for server and client respectively.

Then, start mongodb service with `sudo service mongod start` and then finally run the following command from inside the `server` directory.

- `npm run dev`

This will start both the client (port 3000) and server (port 5000) and launch the site in port 3000. Then navigate to one of the below.

#### `npm test`

Launches the test runner in the interactive watch mode.<br>

## Could NOT deploy to Heroku - details below and All Trials were made in the other duplicate directory (material-ui-table-with-node-mongodb-duplicate-FOR-FAILED-HEROKU-TRIALS), where everything is exact same, only the directory structure is DIFFERENT. Meaning, there, I dont have a separate `server` directory to hold all the server code. ( Have kept the file-tree structure just the same, as my Dev-Book code, which is also a MERN stack app, and successfully deployed in Heroku )

Main failure reason and Errors I got in the Terminal -

**at=error code=H20 desc="App boot timeout"**

**Process running mem=567M(110.8%)**
**Error R14 (Memory quota exceeded)**

**Error R10 (Boot timeout) -> Web process failed to bind to \$PORT within 60 seconds of launch**

**H10 - App crashed** - A crashed web dyno or a boot timeout on the web dyno will present this error.

### Some more explanation on the failure

1> https://stackoverflow.com/questions/43903320/error-in-heroku-when-deploying-react-node-app

You are getting "Error R14 (Memory quota exceeded)". [Check R14 - Memory Quota Exceeded](https://devcenter.heroku.com/articles/error-codes#r14-memory-quota-exceeded) to see some possible tips. Perhaps you have packed in too much functionality into a single dyno? What does your Procfile look like, and what dyno types are you using?

2> It also could be that Heroku does not support mongocluster (which is where I have hosted my database) - As Heroku specifically gives an addon for mLab, but does not give anything for mongocluster.

### Have unsuccessfully tried the following configuration in package.json file's scripts codes

````js
"heroku-postbuild": "cd client && npm install && npm run build",

"heroku-postbuild": "NPM_CONFIG_PRODUCTION=false npm install --prefix client && npm run build --prefix client"

"heroku-postbuild": "cd client && npm install && npm run build",

"start": "node index.js",

"start": "concurrently \"npm run server\" \"npm run client\"",

```

#### Script Configuration - 1 that did not work

```js
"scripts": {
        "client-install": "npm start --prefix client",
        "start": "node index.js",
        "server": "nodemon index.js",
        "client": "npm start --prefix client",
        "dev": "concurrently \"npm run server\" \"npm run client\"",
        "heroku-postbuild": "NPM_CONFIG_PRODUCTION=false npm install --prefix client && npm run build--prefix client ",
        "fix-code": "prettier-eslint --write 'src/**/*.{js,jsx}' ",
        "fix-styles": "prettier-stylelint --write 'src/**/*.{css,scss}' "
    },
````

#### Script Configuration - 2 that did not work (and this is exact same what I had in my DevBook Repo)

```js
"scripts": {
        "client-install": "npm start --prefix client",
        "start": "node index.js",
        "server": "nodemon index.js",
        "client": "npm start --prefix client",
        "dev": "concurrently \"npm run server\" \"npm run client\"",
        "heroku-postbuild": "cd client && npm install && npm run build",
        "fix-code": "prettier-eslint --write 'src/**/*.{js,jsx}' ",
        "fix-styles": "prettier-stylelint --write 'src/**/*.{css,scss}' "
    },

```