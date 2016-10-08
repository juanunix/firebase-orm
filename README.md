# Firebase ORM

This is an extension to the Firebase JavaScript library to manage relations between users, objects, and servers. It defines a security model, relationship-mapping scheme, and 

- [Security](#Security)
- [Database](#Database)
- [Object](#Object)


# Object

Objects in the ORM are represented by Firebase references (`firebase.database.Reference`). A reference to an object with a certain **type** and **id** is the path `/data/type/id`. 

Data contained within the object is stored in the `data` path, so `/data/type/id/data` is final path to the underlying data.

References to children objects are stored under the `child` path, where `/data/type/id/child/childType/childId` is set to true to indicate a parent-child relationship between the (type, id) object and the (childType, childId) object.

Read/write privileges are stored under the `read` and `write` path, where the `uid` of a user authorized to read the object is mapped to the value `true`.

The additional reference methods assume the reference is to the root location of a Firebase object. Every object has a string **type** and a unique **id** for that type. 

```
var ref = // get a reference to an object
ref.getType()     // 'comment'
ref.getId()       // '-KTWRYiYxUbSqtBf'
```

### .isObject()

Returns true if this is an object reference, false otherwise.

### .getType()


## firebase.database.Database

### .add(type)

Create a new object with `.add(type)`. This returns a reference to the object's Firebase location.

```javascript
var commentRef = firebase.database().add('comment');

commentRef.toString()   // <FIREBASE URL>/data/comment/-KTWRYiYxUbSqtBf
```

### .get(type, id)

Returns a reference to the root of the database object with the given type and id.

### .each(type, callback)

Iterate over each object of a given type with `.each(type)`. Admin sees every object, regular user only sees the ones they own

### .getUser(callback)

Returns the user object

