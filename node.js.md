### Error

1. /usr/bin/env: ‘node’: No such file or directory
* solution: 
```
$ ln -s /usr/bin/nodejs /usr/bin/node
```

### 삭제
```
$ sudo apt-get remove nodejs
$ sudo apt-get remove npm
$ sudo apt-get update
```
* Check for any .npm or .node folder in your home folder and delete those.
```
$ which node
$ which nodejs
$ which npm
```
* This is better to remove NodeJS and its modules manually because installation leaves a lot of files, links and modules behind and later it create problems while we reconfigure another version of NodeJS and its modules. Run the following commands.
```
$ sudo rm -rf /usr/local/bin/npm /usr/local/share/man/man1/node* /usr/local/lib/dtrace/node.d ~/.npm ~/.node-gyp /opt/local/bin/node /opt/local/include/node /opt/local/lib/node_modules 
$ sudo rm -rf /usr/local/lib/node*
$ sudo rm -rf /usr/local/include/node*
$ sudo rm -rf /usr/local/bin/node*
```
