# Full-stack App Initial Setup
The following provides basic instructions for setting-up a full-stack app using the PERN stack. It assumes familiarity with the computer's terminal and also assumes that PostgreSQL, Express, React and Node, as well as Sequelize, have already been installed on your computer. The intent of the repository is to serve as a reference for running the multiple commands and establising the required dependencies for any PERN stack project. 

## Create Root Directory
In the computer's terminal, make a new root directory for the project and name it. For this example, the root directory is named "fullstack_app." Run this command:<br>
`mkdir fullstack_app`
<br>
<br>
Next, change into the new directory `fullstack_app` and create a directory for all of the back-end files. In this example, it is named "api," but you can name it whatever suits your project. Run this command:<br>
`mkdir api`

## Prepare Backend Directory & Create Database
### Initial Installations
First, change into the `api` directory, and then do the following:
1. Create an entry point file (server.js or app.js): `touch app.js`
2. Initialize the project with Node: `npm init -y`
3. Install PERN dependencies: `npm i pg sequelize express cors`
4. Install Nodemon: `npm install nodemon --save-dev`

### Update package.json
Next, open VS Code `code .` and click on the `package.json` file. Add these scripts to the `package.json` file to set up the server:
```javascript
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
```
### Create the Database
1. First, initialize Sequelize in the terminal: `sequelize init`
2. Next, open the `config.json` file in VS Code and update the `"development"` object:
  * Update dialect: `"dialect": "postgres"`
  * Rename the `"database"` to match your project theme
  * If necessary, change `"username"` from `"root"` to `"postgres"`
  * If necessary, change `"password"` to your postgresSQL password, BUT BE SURE to change this back to `"null"` BEFORE any add, commit or push to Git.
3. Create the database from the terminal: `sequelize db:create`

Congratulations! The intial backend set up is complete, and the database has been created.

### Node Modules
One last bit of housekeeping is helpful to include here before moving forward. To prevent unnecessary files (i.e. node modules) from being pushed to remote repositories, create a "gitignore" file.

In the terminal, create a `.gitignore` file to store the `node_modules`:
  * Run `touch .gitignore`
  * Then run `echo node_modules > .gitignore`


### Create & Associate Models
The following steps assume that you have already determined:
  * The number of models needed for your project
  * The data fields and corresponding datatypes to structure each model
  * The relationships between the different models have been mapped out

#### MODELS
First, create a model in the terminal. Each model requires a name and set of attributes; this example is named "User" and will collect relevant user data. Run this command: `sequelize model:generate --name User --attributes first_name:string,last_name:string,age:integer`

A couple points to note regarding the syntax of this command:<br>
* `name` of the model - `User` in this example - is `PascalCase` and typically singular
* `attributes` defines the fields of the model and the respective datatypes; the syntax must be free of spaces and must be written in `snakecase` and `under_scored`.

Next, open VS Code and click on one of the models you created, "User" in this example. Then do the following:
1. Scroll down to the section "User.init." After "modelName: 'User', add `tableName: 'users'`
```javascript
User.init({
  first_name: DataTypes.STRING,
  last_name: DataTypes.STRING,
  age: DataTypes.INTEGER
}, {
  sequelize,
  modelName: 'User',
  tableName: 'users'
});
```
2. Next, click on the related migration file, which in this example will be a labeled "create-user.js". We need to change the table name in our async functions to match our model:
  * In the `async up` function change `Users` to `users`
  * In the `async down` function change `Users` to `users`

#### ASSOCIATIONS
Once the models are generated, they can be associated. Sequelize documentation provides information about the four types of associations, as well as instructions to set them up. Visit https://sequelize.org/docs/v6/core-concepts/assocs/ for more information. 

#### MIGRATE
Migrate the database in the terminal: `sequelize db:migrate`

### Create Routes & Controllers
In the `api` directory create a directory for routes and one for controllers: `mkdir routes controllers`

#### ROUTES
1. Change to the `routes` directory and make a new file: `touch AppRouter.js`
2. In VS Code, open the server point of entry file which is `app.js` in this example. Insert the boilerplate: 
```javascript
const express = require('express')
const cors = require('cors')

const app = express()

const AppRouter = require('./routes/AppRouter')

const PORT = process.env.PORT || 3001

app.use(cors())
app.use(express.json())
app.use(express.urlencoded({ extended: true }))

app.get('/', (req, res) => res.json({ message: 'Server Works' }))
app.use('/api', AppRouter)
app.listen(PORT, () => console.log(`Server Started On Port: ${PORT}`))
```
3. In the `AppRouter.js` file set up the routes variables and functions.
4. In the routes directory create a new route: `touch UserRouter.js`
5. Set up the `UserRouter.js` file
6. Add `UserRouter` to the `AppRouter.js` file

#### CONTROLLERS
1. Change to the `controllers` directory and add controllers: `touch UserController.js`
2. Set up the `UserController.js` file



## React Set Up
1. Change to the root directory `fullstack_app`
2. Create a react app: `npx create-react-app client`
3. Next install axios: `npm install axios`




