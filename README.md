# Full-stack App Initial Setup
Basic set up instructions for building a full-stack app using the PERN stack and React.js

## Step 1 - Create Root Directory
1. Make a new root directory for the project: `mkdir fullstack_app`
2. Change into the new directory `fullstack_app` and create a sub-directory for the back end: `mkdir api`

## Step 2 - Prepare Back-end Directory
### Part 1 - Install, Initialize & Create Database
1. Change into the back-end directory `api`
2. Create an entry point file (server.js or app.js): `touch app.js`
3. Initialize the project with Node: `npm init -y`
4. Install PERN dependencies: `npm i pg sequelize express cors`
5. Install Nodemon: `npm install nodemon --save-dev`
6. Open VS Code: `code .`
7. Open the `package.json` file and add scripts to set up the server:
```javascript
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
```
8. Initialize Sequelize in the terminal: `sequelize init`
9. Open the `config.json` file in VS Code and update the `"development"` object:
  * Update dialect: `"dialect": "postgres"`
  * Rename the `"database"` to match your project theme
  * If necessary, change `"username"` from `"root"` to `"postgres"`
  * If necessary, change `"password"` to your postgresSQL password, BUT BE SURE to change this back to `"null"` BEFORE making and add, commit or push to Git.
10. Create the database from the terminal: `sequelize db:create`
11. In terminal, create a `.gitignore` file to store the `node_modules`:
  * Run `touch .gitignore`
  * Then run `echo node_modules > .gitignore`

### Part 2 - Create & Associate Models
1. Create models in the terminal: `sequelize model:generate --name User --attributes first_name:string,last_name:string,age:integer`
    * `name` of the model - `User` in this example - is `PascalCase` and typically singular
    * `attributes` defines the fields of the model and the respective data types; the syntax must be free of spaces and must be written in `snakecase` and `under_scored`.
2. Once the models are generated, make associations between them: e.g. `hasMany` and `belongsTo`
3. In models, add `tableName: `users`
4. In the migration file, change `Users` to `users` in the `async up` and `async down` functions. 
5. Migrate the database in the terminal: `sequelize db:migrate`

### Part 3 - Create Routes & Controllers
1. In the `api` directory create a folder for routes and controllers: `mkdir routes controllers`
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




