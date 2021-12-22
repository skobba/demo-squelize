# Setup
```
mkdir demo-sequelize
cd demo-sequelize
npm init -y
npm install sequelize pg
npm install --save-dev sequelize-cli
```

Next we will initialize a Sequelize project, then open the directory in our code editor:
```
npx sequelize-cli init
```

# Create root user
```
CREATE USER root;
ALTER USER root WITH SUPERUSER;
```

# Create Database
```
npx sequelize-cli db:create
```

# Create a User model
```
npx sequelize-cli model:generate --name User --attributes firstName:string,lastName:string,email:string,password:string
```

# Execute Migration
```
npx sequelize-cli db:migrate
```

# Create Seeder
```
npx sequelize-cli seed:generate --name user
```

# Execute the Seeder
```
npx sequelize-cli db:seed:all
```

# Check if it´s data in the Users table
```
psql sequelize_project_development
SELECT * FROM "Users";
```

# Adds two columns to Users table
## Create a new Migration Skeleton
```
npx sequelize-cli migration:generate --name migration-skeleton
```

## Edit the new Migration Skeleton file
```js
  up: (queryInterface, Sequelize) => {
    return queryInterface.sequelize.transaction(t => {
      return Promise.all([
        queryInterface.addColumn('Users', 'petName', {
          type: Sequelize.DataTypes.STRING
        }, { transaction: t }),
        queryInterface.addColumn('Users', 'favoriteColor', {
          type: Sequelize.DataTypes.STRING,
        }, { transaction: t })
      ]);
    });
  },
  down: (queryInterface, Sequelize) => {
    return queryInterface.sequelize.transaction(t => {
      return Promise.all([
        queryInterface.removeColumn('Users', 'petName', { transaction: t }),
        queryInterface.removeColumn('Users', 'favoriteColor', { transaction: t })
      ]);
    });
  }
```

## Run Migration (again)
```
npx sequelize-cli db:migrate
```

## Check Result
Describe Users table:
```
\d "Users"
```
