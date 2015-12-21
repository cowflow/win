/*
 // Store 'marcus' at 'username'
 store.set('username', 'marcus')

 // Get 'username'
 store.get('username')

 // Remove 'username'
 store.remove('username')

 // Clear all keys
 store.clear()

 // Store an object literal - store.js uses JSON.stringify under the hood
 store.set('user', { name: 'marcus', likes: 'javascript' })

 // Get the stored object - store.js uses JSON.parse under the hood
 var user = store.get('user')
 alert(user.name + ' likes ' + user.likes)

 localStorage calls toString on all values that get stores. This means that you can't conveniently store and retrieve numbers, objects or arrays:

 localStorage.myage = 24
 localStorage.myage != 24
 localStorage.myage == '24'

 localStorage.user = { name: 'marcus', likes: 'javascript' }
 localStorage.user == "[object Object]"

 localStorage.tags = ['javascript', 'localStorage', 'store.js']
 localStorage.tags.length == 32
 localStorage.tags == "javascript,localStorage,store.js"
 What we want (and get with store.js) is

 store.set('myage', 24)
 store.get('myage', 24) == 24

 store.set('user', { name: 'marcus', likes: 'javascript' })
 alert("Hi my name is " + store.get('user').name + "!")

 store.set('tags', ['javascript', 'localStorage', 'store.js'])
 alert("We've got " + store.get('tags').length + " tags here")

 */


var store = (function () {
    var api               = {},
        win               = window,
        doc               = win.document,
        localStorageName  = 'localStorage',
        globalStorageName = 'globalStorage',
        storage;

    api.set    = function (key, value) {};
    api.get    = function (key)        {};
    api.remove = function (key)        {};
    api.clear  = function ()           {};

    if (localStorageName in win && win[localStorageName]) {
        storage    = win[localStorageName];
        api.set    = function (key, val) { storage.setItem(key, val) };
        api.get    = function (key)      { return storage.getItem(key) };
        api.remove = function (key)      { storage.removeItem(key) };
        api.clear  = function ()         { storage.clear() };

    } else if (globalStorageName in win && win[globalStorageName]) {
        storage    = win[globalStorageName][win.location.hostname];
        api.set    = function (key, val) { storage[key] = val };
        api.get    = function (key)      { return storage[key] && storage[key].value };
        api.remove = function (key)      { delete storage[key] };
        api.clear  = function ()         { for (var key in storage ) { delete storage[key] } };

    } else if (doc.documentElement.addBehavior) {
        function getStorage() {
            if (storage) { return storage }
            storage = doc.body.appendChild(doc.createElement('div'));
            storage.style.display = 'none';
            // See http://msdn.microsoft.com/en-us/library/ms531081(v=VS.85).aspx
            // and http://msdn.microsoft.com/en-us/library/ms531424(v=VS.85).aspx
            storage.addBehavior('#default#userData');
            storage.load(localStorageName);
            return storage;
        }
        api.set = function (key, val) {
            var storage = getStorage();
            storage.setAttribute(key, val);
            storage.save(localStorageName);
        };
        api.get = function (key) {
            var storage = getStorage();
            return storage.getAttribute(key);
        };
        api.remove = function (key) {
            var storage = getStorage();
            storage.removeAttribute(key);
            storage.save(localStorageName);
        }
        api.clear = function () {
            var storage = getStorage();
            var attributes = storage.XMLDocument.documentElement.attributes;;
            storage.load(localStorageName);
            for (var i=0, attr; attr = attributes[i]; i++) {
                storage.removeAttribute(attr.name);
            }
            storage.save(localStorageName);
        }
    }
    return api;
})();
