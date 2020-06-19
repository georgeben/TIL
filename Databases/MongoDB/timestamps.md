#### Storing correct local dates
By default, MongoDB stores times in UTC and will convert any local time representations into this form. Most times, the UTC time will be different 
from your local time, for example in Nigeria, UTC is one hour behind our local time. To store the correct local time, you must also store the difference between 
the UTC time and your local time in your model.  

Example
Instead of storing the time this:  
(I'm using [mongoose](https://mongoosejs.com/) for this example, but the concept is still the same)
```js
const yourSchema = new mongoose.Schema({
  lastActive: { // A property to store the time a user was last active
    type: Date,
    required: true,
    default: new Date(),
  },
})

```
Do this to store the local time
```js
const yourSchema = new mongoose.Schema({
  lastActive: { 
    type: Date,
    required: true,
    default: new Date(),
  },
  lastActiveOffset: {
    type: Number,
  }
});
yourSchema.pre('save', function (next) {
  this.lastActiveOffset = this.lastActive.getTimezoneOffset()
  next();
})
module.exports = mongoose.model('YourModel', yourSchema)
```
To calculate your local time do:
```js
 const localTime = new Date( yourModel.lastActive.getTime() -  ( yourModel.lastActiveOffset * 60000 ) );
 // And this gives you the correct local time 
```
