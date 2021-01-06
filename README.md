# MERN_Stack_Udemy
==================

npm install express express-validator bcryptjs config gravatar jsonwebtoken mongoose request
npm install -D nodemon concurrently 

execute : npm run server
===================================================================================
***********************************************************************************
===================================================================================

express-validator
=================
documentation : https://express-validator.github.io/docs/
used in file : MERN_Stack_Udemy\routes\api\users.js
and code is 
---------------------------------------------------------------------------------------------------
users.js
--------
const express= require('express');
const router= express.Router();
const {check,validationResult} = require('express-validator/check');


// @route  POST api/users
// @desc   Register User
// @access Public

router.post('/' , [
    check('name','Name is required').not().isEmpty(),
    check('email','Please include a valid email').isEmail(),
    check('password','Please enter a password with 6 or more characters').isLength({
        min:6
    })
],(req,res) => {
    const errors = validationResult(req);
    if(!errors.isEmpty()){
        return res.status(400).json({errors:errors.array()});
    }
    res.send('User Route');
});

module.exports = router;
---------------------------------------------------------------------------------------------------

Postman :
http://localhost:5050/api/users
select : POST
body :{
	"name" : "swatantra sinha",
	"email" : "swat1508@gmail.com",
	"password": "swat"
}

output :
{
    "errors": [
        {
            "value": "swat",
            "msg": "Please enter a password with 6 or more characters",
            "param": "password",
            "location": "body"
        }
    ]
}
===================================================================================
***********************************************************************************
===================================================================================

User Registration
-----------------
// See if user exists
// get users gravatar
// encrypt password
// return jsonwebtoken


===================================================================================
***********************************************************************************
===================================================================================

After end of section 3(means Lec 14)
------------------------------------
In postman we can perform following requests (saved in POSTMAN in folder "users and auth") :

1. Register User
type - POST
URL - http://localhost:5050/api/users
Header : Content-Type and value as "application/json"
body : 
{
	"name" : "swatantra sinha",
	"email" : "swat1508@gmail.com",
	"password": "sinha1508"
}

response : {token : <token_value>}

2. Get Auth User
type - GET
URL - http://localhost:5050/api/auth
Header : x-auth-token 
and value as token from above 

response :
{
    "_id": "5ff5d8f4df33e240385262db",
    "name": "swatantra sinha",
    "email": "swat1508@gmail.com",
    "avatar": "//www.gravatar.com/avatar/6319a12b0905aa50a3ba56146b3ee61c?s=200&r=pg&d=mm",
    "date": "2021-01-06T15:36:20.482Z",
    "__v": 0
}


3. Login User
type - POST
URL - http://localhost:5050/api/auth
Header : Content-Type and value as "application/json"
body : 
{
	"email" : "swat1508@gmail.com",
	"password" : "sinha1508"
}

response : {token : <token_value>}
