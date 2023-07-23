# Mongodb Cheatsheet

This page presents a list of commonly used commands in mongodb.

---
# Install
## ubuntu 20.04 (Focal)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update && sudo apt-get install -y mongodb-org
```

## ubuntu 18.04 (Bionic)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update && sudo apt-get install -y mongodb-org
```

## ubuntu 16.04 (Xenial)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update && sudo apt-get install -y mongodb-org
```

## debian 11 (Bullseye)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb http://repo.mongodb.org/apt/debian bullseye/mongodb-org/6.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update && sudo apt-get install -y mongodb-org
```

## debian 10 (Buster)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/6.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update && sudo apt-get install -y mongodb-org
```

## debian 9 (Stretch)

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb http://repo.mongodb.org/apt/debian stretch/mongodb-org/6.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update && sudo apt-get install -y mongodb-org
```

---
# Uninstall

```bash
# Stop mongodb.
sudo service mongod stop

# Remove mongodb.
sudo apt-get purge mongodb-org*

# Remove data directory.
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```

---
# Mongodb Service Managament

```bash
# Start mongodb.
sudo systemctl start mongod

# If you see error like this "Failed to start mongod.service: Unit mongod.service not found.", run
sudo systemctl daemon-reload

# Enable mongodb as a service which starts after reboot.
sudo systemctl enable mongod

# Stop monogdb service.
sudo systemctl stop mongod

# Check mongodb service status.
sudo systemctl status mongod

# Restart mongodb.
sudo systemctl restart mongod

# Ping mongodb.
mongo --eval 'db.runCommand({ connectionStatus: 1 })'

# Connect to mongodb service from mongodb shell.
mongosh
```

---
# DB Shell Commands
## DB Commands

```cpp
// Show all databases.
show dbs

// Show the current database.
db

// Create or switch database. (Replace db_name with yours)
use db_name

// Drop the current database.
db.dropDatabase()
```

## Collection Commands

```cpp
// Create collection. (Replace col_name with yours)
db.createCollection(col_name)

// Show collections.
show collections

// Insert one row. (Replace json with yours)
db.col_name.insert({
    key1: "value1",
    key2: "value2"
})

// Insert many rows. (Replace json with yours)
db.col_name.insertMany([
    {
        key1: "value1_1",
        key2: "value1_2"
    },
    {
        key1: "value2_1",
        key2: "value2_2"
    }
])

// Get all rows.
db.col_name.find()

// Get all rows formated.
db.col_name.find().pretty()

// Find one row.
db.col_name.findOne({
    key1: "value1"
})

// Find rows with specific fields.
db.col_name.find({ key1: "value1" }, {
  key1: 1,
  key2: 1
})

// Find rows.
db.col_name.find({
    key1: "value1"
})

// Update one row.
db.col_name.updateOne(
    { key1: "value1" },
    {
        "$set": {
            key1: "value1",
            key2: "value3"
        }
    },
    {
        upsert: true
    }
)

// Update many rows.
db.col_name.updateMany(
    { key1: "value1" },
    {
        "$set": {
            key1: "value1",
            key2: "value3"
        }
    },
    {
        upsert: true
    }
)

// Delete row.
db.col_name.remove({
    key1: "value1"
})

// Sort rows.
db.col_name.find().sort({ key1: 1 })

// Count rows.
db.col_name.find().count()

// Limit rows.
db.col_name.find().limit(2)

// For each.
db.col_name.find().forEach(function(obj) {
    print("Object: " + obj.key1)
})

// Create index.
db.col_name.createIndex({
    key1: 1
})
```

---
# Files

File Path|File Use
---|---
`/etc/mongod.conf`|default config file path
`/var/log/mongodb/mongod.log`|default log file path

[Back to CheatSheets Page](https://phucbone.github.io/Cheatsheets/)

[Back to Main Page](https://phucbone.github.io/)
