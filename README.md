# MERN_Stack_Udemy


npm install express express-validator bcryptjs config gravatar jsonwebtoken mongoose request
npm install -D nodemon concurrently 
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
    console.log('check');
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