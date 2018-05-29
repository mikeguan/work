对database进行重命名操作，但因为MongoDB并没有提供renameDatabase的命令，用户的想法是通过copydb来实现，先将数据库拷贝一份，然后删除老的数据库，但由于DB里数据很多，copydb太耗时，想知道是否有更好的方法？

虽然MongoDB没有renameDatabase的命令，但提供了renameCollection的命令，这个命令并不是仅仅能修改collection的名字，同时也可以修改database。
```
db.adminCommand({renameCollection: "db1.test1", to: "db2.test2"})
```
上述命令实现了将db1下的test1，重命名为db2下的test2，这个命令只修改元数据，开销很小，有了这个功能，要实现db1重命名为db2，只需要遍历db1下所有的集合，重命名到db2下，就实现了renameDatabase的功能，写个js脚本能很快的实现这个功能.
```
var source = "source";
var dest = "dest";
var colls = db.getSiblingDB(source).getCollectionNames();
for (var i = 0; i &lt; colls.length; i++) {
    var from = source + &quot;.&quot; + colls[i];
    var to = dest + &quot;.&quot; + colls[i];
    db.adminCommand({renameCollection: from, to: to});
}
```
