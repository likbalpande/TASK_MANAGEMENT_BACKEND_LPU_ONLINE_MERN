### STEP 1. 
    npm init -y
### STEP 2.
    npm i express mongodb mongoose nodemon dotenv cors bcrypt cookie-parser morgan jsonwebtoken

### STEP 3.
    Make folders "config", "models"

### STEP 4.
    make a .gitignore --> 
    `node_modules 
    .env
    `

### STEP 5.
    make a .env file -->
    `MONGO_DB_URL=
    MONGO_DB_PASSWORD=
    MONGO_DB_DATABASE_NAME=
    `

(if you don't have mognodb account --> create the account --> select FREE when you get the deployment option and "create deployment")
(wait for 5 minutes for cluster to get created)
go to "network access" in left panel --> add ip address --> allow access from any where --> done

go to "database access" in left panel --> edit --> edit password --> type new password --> update user 
(this is your MONGO_DB_PASSWORD value)

go to "clusters" in left panel --> "connect" --> select drivers --> copy link in 3rd step 
(this is your MONGO_DB_URL)

MONGO_DB_DATABASE_NAME=write any name according to you but no space or hyphen 

for example,
MONGO_DB_URL=mongodb+srv://likhileshbalpande:<db_password>@cluster0.abcdx.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0
MONGO_DB_PASSWORD=mypasshardword
MONGO_DB_DATABASE_NAME=LPU_TASK_MANAGEMENT_MERN_ONLINE

### STEP 6.
    Inside config --> dbConfig.js -->

    `const mongoose = require("mongoose");

    const URL = process.env.MONGO_DB_URL;
    const URL_WITH_PASSWORD = URL.replace("<db_password>", process.env.MONGO_DB_PASSWORD);
    const URL_WITH_PASSWORD_AND_DB_NAME = URL_WITH_PASSWORD.replace("/?", `/${process.env.MONGO_DB_DATABASE_NAME}?`);

    const connectToDb = async () => {
        try {
            await mongoose.connect(URL_WITH_PASSWORD_AND_DB_NAME);
            console.log("--------- MONGO_DB CONNECTED ---------");
        } catch (err) {
            console.log("------ MONGO_DB NOT CONNECTED --------");
            console.log(err.message);
        }
    };

    connectToDb(); 
    `

### STEP 7.
    Make app.js file --> 
    `
    `

### STEP 8.
    run the application to check if it is working-->
    npx nodemon app.js

## HTTP STATUS CODES
(https://static.semrush.com/blog/uploads/media/3a/79/3a7950050980a0e2de37bc1a632cc321/wmkPPztB7KlAC7fPzO0-85NG8t0B9IEh4JEbt_ELP1pvJMhof9vt2pDSwrBZeXodoqaoV_Es1Rur-AWoeoOdV-RIde2vjqyMQuxrqch62uXZ1bsI0yaaMWx-f4cg4BlmOQrI2kFJ6CPXECCd69KeopE.png)
    
    1XX --> nothing imp for you
    
    3XX --> nothing imp for you

    2XX --> success -->
        200 --> OK (In general)
        201 --> created (CREATE / POST)
        204 --> No content (DELETE)
    
    4XX --> mistake of client
        400 --> bad request (validation error, or something is missing which was required, ...)
        401 --> unauthorized (the user does not have permission)
        404 --> NOT FOUND (this you will mostly get in express app when the endpoint or route you are using is not attached on the app)
                you may send it when the user asked for something which is not present

    5XX --> mistake of server
        500 --> Internal Server Error (Something went wrong on server that code was not prepared for )
            (connection issue, ram outage, processor outage, or ...)
    

### STEP 9.
    Make a userModel.js file -->
    // 1. make a schema
    // 2. make a model --> attached to a collection and schema
    // then use this model anywhere to work on the collection like find documents, add document, delete document, update document
    
### STEP 10.
    Make a BASIC post api to create a BASIC user

### STEP 11.
    IMPORTANT STEP: to do in app.js: 
    add these middlewares to your code -->
    `
        ...
        const cors = require("cors"); // this allow the browser to enable frontend to connect to backend by giving such permissions
        ...
        ...
        app.use(cors()); // this code actually allows all origins / domains to talk with backend
        app.use(express.json()); // this will read the request body stream and serializes it into javascript object and attach it on the req object 
        ...
    `

## HTTP METHODS or VERBS : 
* GET : Read / Search / Find
* POST : Create / make new entry in DB
* PATCH : Edit a part of data
* PUT : Edit the data but at a level where it equivalent to replace
* DELETE :  Delete something from database

* (https://medium.com/@hhphu/understanding-http-verb-tampering-in-web-security-e2a167a9917e)

## how view database ?  collections ? documents
--> go to "clusters" in left panel --> click on "browse collections" --> select your database --> select your collection --> now you will see all your documents


## Validation Keywords
* type: mentions the data type for the value (it is mandatory in every property in schema)
`   age: {
        type: Number,
    },
`
`    
    age: Number,
`
in the second part, the limitation is you cannot add more validators
if you want to add more validators other than type, then use "{" "}"

* required: it mentions that the key should always be present in every entry that is made to the database
* trim: removes the whitespaces, tabs, new lines at start & end (if any)
* unique: it enforces that the value in this field should be unique in the given collection
* enum: allowed options as value (you can only choose from these options (case-sensitive))
* default: it gives the default value to the key when it is not present 
(age: null) - then age will not get default value because null is also a value
(anything that is undefined is considered as absent) 
(age: undefined)
* min
* max
* minLength
* maxLength
* match
( Article to refer: https://mongoosejs.com/docs/validation.html )