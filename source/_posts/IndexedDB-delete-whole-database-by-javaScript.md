---
title: IndexedDB-delete whole database by javaScript
catalog: true
date: 2019-10-28 14:24:15
subtitle:
header-img:
tags:
- IndexedDB
categories:
- TECH
- FrontEnd
- Browser Caching
- IndexedDB
---

# 使用[indexedDB.deleteDatabase](https://developer.mozilla.org/en-US/docs/Web/API/IDBFactory/deleteDatabase)：

```javaScript
var DBDeleteRequest = window.indexedDB.deleteDatabase("toDoList");

DBDeleteRequest.onerror = function(event) {
  console.log("Error deleting database.");
};
 
DBDeleteRequest.onsuccess = function(event) {
  console.log("Database deleted successfully");
    
  console.log(event.result); // should be undefined
};

// you must call db.close() before delete, if you already open. otherwise you will get onblocked event
DBDeleteRequest.onblocked = function () {
    console.log("Couldn't delete database due to the operation being blocked");
};
```
# indexedDB.[databases()](developer.mozilla.org/en-US/docs/Web/API/IDBFactory/databases)
可以使用indexedDB.databases() 得到所有的databases List.
如果这个数据库已经open过，在删除数据库前需要调用[db.close() ](https://developer.mozilla.org/en-US/docs/Web/API/IDBDatabase/close) 否则onblocked event会触发。
```javaScript
return window.indexedDB.databases()
    .then((dbs) => {
        dbs.map(db => {
            db.close();
            window.indexedDB.deleteDatabase(db.name)
        })
    }).catch(console.error);
```
indexedDB.databases() 有一个很大问题就是支持的浏览器太少了。只有Chrome和Opera能很好的支持，IE11, Firefox, Safari都不太支持。


实例：删除除了此user的所有其他IndexedDB
```javaScript

  /**
   * Checks IndexedDB for all IndexedDBs and deletes them if the username
   * is not the one provided. Used when changing users after session expires.
   *
   * @static
   * @param {String} usernameToKeep Current authenticated user
   * @returns
   * @memberof DB
   */
  static purgeIndexedDB(usernameToKeep) {
    if (window.indexedDB && window.indexedDB.databases) {
      return window.indexedDB.databases()
        .then((dbs) => 
            dbs.filter((db) => (db.name.includes('_pouch_') && (!usernameToKeep || !db.name.includes(usernameToKeep)))))
        .then((IndexedDBS) => 
            Promise.all(IndexedDBS.map((IndexedDB) => window.indexedDB.deleteDatabase(IndexedDB.name))))
        .catch(console.error);
    }
    return false;
  }
```

# Reference Links:

* [How can I remove a whole IndexedDB database from JavaScript?](https://stackoverflow.com/questions/15861630/how-can-i-remove-a-whole-indexeddb-database-from-javascript#)
* [indexedDB.databases()](developer.mozilla.org/en-US/docs/Web/API/IDBFactory/databases)
* [indexedDB.deleteDatabase](https://developer.mozilla.org/en-US/docs/Web/API/IDBFactory/deleteDatabase)
* [db.close() ](https://developer.mozilla.org/en-US/docs/Web/API/IDBDatabase/close)