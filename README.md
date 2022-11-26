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
The following steps assume that these details have already been determined:
  * Number of tables or models needed for your project
  * Data and datatypes to be stored in the models
  * Relationships between models have been mapped out


1. Create models in the terminal: `sequelize model:generate --name User --attributes first_name:string,last_name:string,age:integer`
    * `name` of the model - `User` in this example - is `PascalCase` and typically singular
    * `attributes` defines the fields of the model and the respective data types; the syntax must be free of spaces and must be written in `snakecase` and `under_scored`.
2. Once the models are generated, make associations between them: e.g. `hasMany` and `belongsTo`
3. In models, add `tableName: `users`
4. In the migration file, change `Users` to `users` in the `async up` and `async down` functions. 
5. Migrate the database in the terminal: `sequelize db:migrate`

### Create Routes & Controllers
1. In the `api` directory create a directory for routes and one for controllers: `mkdir routes controllers`
2. Change to the `routes` directory and make a new file: `touch AppRouter.js`
3. In VS Code open the server point of entry file which is `app.js` in this example. Insert the boilerplate.
4. In the `AppRouter.js` file set up the routes variables and functions.
5. In the routes directory create a new route: `touch UserRoute.js`
6. Change to the `controllers` directory and add controllers: `touch UserController.js`
7. Set up the `UserController.js` file
8. Set up the `UserRouter.js` file
9. Add `UserRouter` to the `AppRouter.js` file

## Step 2 - React Set Up
1. Change to the root directory `fullstack_app`
2. Create a react app: `npx create-react-app client`
3. Next install axios: `npm install axios`




