# Pet-Store API Meta-System
This project is a practical implementation of the [PetStore API](https://petstore.swagger.io) in Meta-System. You can use it as a base to create your own system or even just clone this repo and test it for fun.

## Running this System
**Requirements**
- Having nodejs installed (12.x or greater)
- Installing Meta-System with npm (`npm install -g meta-system`)
- Have an instance of MongoDB running with the right credentials

After all the requirements are met, just run `meta-system ./petstore.json` while in the root of this repo.

## Setting up the Database
We need to have an instance of MongoDB running, and it must have an user with the right permissions and credentials. These instructions are valid only for MongoDB version 5.x or greater.

1. First, install MongoDB in your system according to their [website instructions](https://docs.mongodb.com/manual/administration/install-community/).
1. After that is done, create `mongod.conf` file to have the base configuration of your database saved and ready to go. The details on thw available parameters for that file [are here](https://docs.mongodb.com/manual/reference/configuration-options/). There is also an `example.mongod.conf` file in this repository, which you can use as a base to configure your database, just changing the needed parts.
1. Change the `path` property on that file to a valid path in your computer.
1. Change the `security > authorization` value to `disabled`. We will enable it again after we create our user.
1. Run your database with `mongod --config </path/to/your/config>`. The part between `<>` is the path of your database configuration file.
1. Open another terminal window and access your running database with the `mongosh --port 27017` command. The `port` option should match what you have set up in the other steps.
1. Type in the command `use("admin")` to switch to the Admin database. We will use this to create our database user.
1. Type in this one line command `db.createUser({ user: "petStore", pwd: "1234", roles: [ {role: "userAdminAnyDatabase", db:"admin"}, {role:"readWriteAnyDatabase", db:"admin"} ] })`. This creates the user we will use for our server. You may change the `user` and the `pwd` values, but be sure to change them to the same value in the `dbConnectionString` value of the `petstore.json` file.
1. Stop your database.
1. Change `security > authorization` back to `enabled`.
1. Run your database again with `mongod --config </path/to/your/config>`.

Every subsequent start of the database will not require any other change, just execute the last step of the process above.
