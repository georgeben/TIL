#### Dependency injection (DI)
DI occurs when the dependencies a service requires to perform it's fucntions are supplied when it is called. For example if a function needs a DB connection to perform it's function, instead of importing the DB connection into the file where the function is situated,
we could simple state that the funtion requires a db connection, which must be supplied whenever it is called. DI makes testing easier, produces a less coupled codebase which is easier to maintain.
Example
```js
// user-service.js
// Non DI approach
const db = require('../../db.js') //Importing the db connection
// Notice that the path to the db is hardcoded, so if we move the db.js file to another location, we have to update all the modules that import the db.js file 😥
module.exports = {
    createUser: (userData) => {
        const user = db.create(userData).... //Create user
    }
}
```
```js
// user-service.js
// A better solution using DI
import assert

module.exports = function({db}){
    assert(db, 'db is required');
    return {
        createUser: (userData) => {
          const user = db.create(userData) // Create user
        }
    }
}
```
The second approach makes life much easier. For example, when testing the user-service.js, we could simply invoke it with a fake db object instead of using modules like sinon to stub the db methods, rewire, proxyquire, etc. This makes testing a lot easier!

**DI is about receiving things instead of taking them**

Useful packages
 - https://www.npmjs.com/package/awilix-express
 - https://www.npmjs.com/package/awilix
 
Related articles
- https://medium.com/@Jeffijoe/dependency-injection-in-node-js-2016-edition-f2a88efdd427 (The 3 parts)
- https://www.freecodecamp.org/news/a-quick-intro-to-dependency-injection-what-it-is-and-when-to-use-it-7578c84fa88f/
- https://medium.com/@magnusjt/dependency-injection-in-nodejs-9601a19c1f36
- https://tsh.io/blog/dependency-injection-in-node-js/

