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
