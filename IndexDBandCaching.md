---
title: JS Notes Index DB and Caching
---

# ***Index DB and Caching***

# **IDB Promise**
localhost:8888/idb-test
npm install
npm run serve

[MDN IDBObjectStore](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore)
[MDN IDBObjectStore.put()](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/put)


## Set up database
```js
// read "hello" in "keyval"
var dbPromise = idb.open('test-db', 1, function(upgradeDb) {
  var keyValStore = upgradeDb.createObjectStore('keyval');
  keyValStore.put("world", "hello");
});
```

## Read from database
[transaction](https://developer.mozilla.org/en-US/docs/Web/API/IDBObjectStore/transaction)
```js
dbPromise.then(function(db) {
  var tx = db.transaction('keyval');
  var keyValStore = tx.objectStore('keyval');
  return keyValStore.get('hello');
}).then(function(val) {
  console.log('The value of "hello" is:', val);
});
```


## Add another value to ObjectStore

```js
// set "foo" to be "bar" in "keyval"
dbPromise.then(function(db) {
  var tx = db.transaction('keyval', 'readwrite');
  var keyValStore = tx.objectStore('keyval');
  keyValStore.put('bar', 'foo');
  return tx.complete;
}).then(function() {
  console.log('Added foo:bar to keyval');
});
```



# Making people and storing them by age / favorite animals

```js

var dbPromise = idb.open('test-db', 4, function(upgradeDb) {
  switch(upgradeDb.oldVersion) {
    case 0:
      var keyValStore = upgradeDb.createObjectStore('keyval');
      keyValStore.put("world", "hello");
    case 1:
      upgradeDb.createObjectStore('people', { keyPath: 'name' });
      //   index on 'people' named 'favoriteAnimal', ordered by 'favoriteAnimal'
    case 2:
      var peopleStore = upgradeDb.transaction.objectStore('people');
      peopleStore.createIndex('animal', 'favoriteAnimal');
    //   index on 'people' named 'age', ordered by 'age'
    case 3:
      var peopleStore = upgradeDb.transaction.objectStore('people');
      peopleStore.createIndex('age', 'age');
  }
});

// read "hello" in "keyval"
dbPromise.then(function(db) {
  var tx = db.transaction('keyval');
  var keyValStore = tx.objectStore('keyval');
  return keyValStore.get('hello');
}).then(function(val) {
  console.log('The value of "hello" is:', val);
});

// set "foo" to be "bar" in "keyval"
dbPromise.then(function(db) {
  var tx = db.transaction('keyval', 'readwrite');
  var keyValStore = tx.objectStore('keyval');
  keyValStore.put('bar', 'foo');
  return tx.complete;
}).then(function() {
  console.log('Added foo:bar to keyval');
});

dbPromise.then(function(db) {
  var tx = db.transaction('keyval', 'readwrite');
  var keyValStore = tx.objectStore('keyval');
  keyValStore.put('Husky', 'favoriteAnimal');
  return tx.complete;
}).then(function() {
  console.log('Added favoriteAnimal:Husky to keyval');
});

// add people to "people"
dbPromise.then(function(db) {
  var tx = db.transaction('people', 'readwrite');
  var peopleStore = tx.objectStore('people');

  peopleStore.put({
    name: 'Sam Munoz',
    age: 25,
    favoriteAnimal: 'dog'
  });

  peopleStore.put({
    name: 'Susan Keller',
    age: 34,
    favoriteAnimal: 'cat'
  });

  peopleStore.put({
    name: 'Lillie Wolfe',
    age: 28,
    favoriteAnimal: 'dog'
  });

  peopleStore.put({
    name: 'Marc Stone',
    age: 39,
    favoriteAnimal: 'cat'
  });

  return tx.complete;
}).then(function() {
  console.log('People added');
});

// list all cat people
dbPromise.then(function(db) {
  var tx = db.transaction('people');
  var peopleStore = tx.objectStore('people');
  var animalIndex = peopleStore.index('animal');

  return animalIndex.getAll('cat');
}).then(function(people) {
  console.log('Cat people:', people);
});

// list all all people ordered by age
dbPromise.then(function(db) {
  var tx = db.transaction('people');
  var peopleStore = tx.objectStore('people');
  var ageIndex = peopleStore.index('age');

  return ageIndex.getAll();
}).then(function(people) {
  console.log('people ordered by age:', people);
});
```

## Cursors
Can be used to change values as you are looping through

```js
// Using cursors
dbPromise.then(function(db) {
  var tx = db.transaction('people');
  var peopleStore = tx.objectStore('people');
  var ageIndex = peopleStore.index('age');

  return ageIndex.openCursor();
}).then(function(cursor) {
  if (!cursor) return;
//   skip first 2 items
  return cursor.advance(2);
}).then(function logPerson(cursor) {
  if (!cursor) return;
  console.log("Cursored at:", cursor.value.name);
  // I could also do things like:
  // cursor.update(newValue) to change the value, or
  // cursor.delete() to delete this entry
  return cursor.continue().then(logPerson);
}).then(function() {
  console.log('Done cursoring');
});
```

# Create database for wittr to store posts

```js
IndexController.prototype._showCachedMessages = function() {
  var indexController = this;

  return this._dbPromise.then(function(db) {
    // if we're already showing posts, eg shift-refresh
    // or the very first load, there's no point fetching
    // posts from IDB
    if (!db || indexController._postsView.showingPosts()) return;

    // TODO: get all of the wittr message objects from indexeddb,
    // then pass them to:
    // indexController._postsView.addPosts(messages)
    // in order of date, starting with the latest.
    // Remember to return a promise that does all this,
    // so the websocket isn't opened until you're done!
    var index = db.transaction('wittrs')
    .objectStore('wittrs').index('by-date');

    return index.getAll().then(function(messages) {
      indexController._postsView.addPosts(messages.reverse());
    });
  });
};

// called when the web socket sends message data
IndexController.prototype._onSocketMessage = function(data) {
  var messages = JSON.parse(data);

  this._dbPromise.then(function(db) {
    if (!db) return;

    var tx = db.transaction('wittrs', 'readwrite');
    var store = tx.objectStore('wittrs');
    messages.forEach(function(message) {
      store.put(message);
    });
  });

  this._postsView.addPosts(messages);
};
```


Show only first 30 posts
```js
IndexController.prototype._onSocketMessage = function(data) {
  var messages = JSON.parse(data);

  this._dbPromise.then(function(db) {
    if (!db) return;

    var tx = db.transaction('wittrs', 'readwrite');
    var store = tx.objectStore('wittrs');
    messages.forEach(function(message) {
      store.put(message);
    });

    // TODO: keep the newest 30 entries in 'wittrs',
    // but delete the rest.
    //
    // Hint: you can use .openCursor(null, 'prev') to
    // open a cursor that goes through an index/store
    // backwards.    
    store.index('by-date').openCursor(null, 'prev')
    .then(function(cursor){
      return cursor.advance(30);
    }).then(function deleteRest(cursor){
      if (!cursor) return;
      cursor.delete();
      return cursor.continue();
    });
  });
  ```

  ## Store Photos

  ```js
  function servePhoto(request) {
  // Photo urls look like:
  // /photos/9-8028-7527734776-e1d2bda28e-800px.jpg
  // But storageUrl has the -800px.jpg bit missing.
  // Use this url to store & match the image in the cache.
  // This means you only store one copy of each photo.
  var storageUrl = request.url.replace(/-\d+px\.jpg$/, '');

  // TODO: return images from the "wittr-content-imgs" cache
  // if they're in there. Otherwise, fetch the images from
  // the network, put them into the cache, and send it back
  // to the browser.
  //
  // HINT: cache.put supports a plain url as the first parameter
  return caches.open(contentImgsCache).then(function(cache){
    return cache.match(storageUrl).then(function(response){
      if (response) return response;
      return fetch(request).then(function(networkResponse){
        cache.put(storageUrl, networkResponse.clone());
        return networkResponse;
      });
    });
  });
}
```

## Cache only NEEDED Imgs
```js
IndexController.prototype._cleanImageCache = function() {
  return this._dbPromise.then(function(db) {
    if (!db) return;

    // TODO: open the 'wittr' object store, get all the messages,
    // gather all the photo urls.
    //
    // Open the 'wittr-content-imgs' cache, and delete any entry
    // that you no longer need.
    var imgsKeep = [];
    var tx = db.transaction('wittrs');
    return tx.objectStore('wittrs').getAll().then(function(messages){
      messages.forEach(function(message){
        if (message.photo){
          imgsKeep.push(message.photo);
        }
      });
      return caches.open('wittr-content-imgs');
    }).then(function(cache){
      return cache.keys().then(function(requests){
        requests.forEach(function(request){
          var url = new URL(request.url);
          if(!imgsKeep.includes(url.pathname)){
            cache.delete(request);
          }
        });
      });
    });
  });
};
```

## Cache Avatars

```js
function serveAvatar(request) {
  // Avatar urls look like:
  // avatars/sam-2x.jpg
  // But storageUrl has the -2x.jpg bit missing.
  // Use this url to store & match the image in the cache.
  // This means you only store one copy of each avatar.
  var storageUrl = request.url.replace(/-\dx\.jpg$/, '');

  // TODO: return images from the "wittr-content-imgs" cache
  // if they're in there. But afterwards, go to the network
  // to update the entry in the cache.
  //
  // Note that this is slightly different to servePhoto!
  return caches.open(contentImgsCache).then(function(cache) {
    return cache.match(storageUrl).then(function(response) {
      var networkFetch = fetch(request).then(function(networkResponse) {
        cache.put(storageUrl, networkResponse.clone());
        return networkResponse;
      });
      return response || networkFetch;
    });
  });
}
```