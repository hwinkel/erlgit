erlgit
======

Erlang convenience wrapper around git executable.

Probably some day it should use geef low-level bindings and expose easy to use API.

Usage
=====

Example of basic usage:
```erlang
1> Local = "/tmp/erlgit".
"/tmp/erlgit"
2> git:clone("http://github.com/gleber/erlgit.git", Local).
{ok,"Cloning into '/tmp/erlgit'...\n"}
3> git:branches(Local).
["master"]
4> git:refs(Local).
[{"HEAD",'HEAD',"097428dda56dec6085747387645d6020f86cfae7"},
 {"master",head,"097428dda56dec6085747387645d6020f86cfae7"},
 {"origin/HEAD",remote, "097428dda56dec6085747387645d6020f86cfae7"},
 {"origin/master",remote, "097428dda56dec6085747387645d6020f86cfae7"},
 {"v0.3.0",tag,"be3b0ade881666286801ee8b218ecbf29da97558"},
 {"v0.3.1",tag,"89f2d81be12f6034db52fd6d71d8a4b96f4ee9de"},
 {"v0.3.2",tag,"3dc42981d9e4677654370614888ec3f368421240"},
 {"v0.5.0",tag,"097428dda56dec6085747387645d6020f86cfae7"}]
5> git:branch(Local).
"master"
6> git:tags(Local).
["v0.3.0","v0.3.1","v0.3.2","v0.5.0"]
7> os:cmd("touch "++Local++"/new_file").
[]
8> git:status_is_dirty(Local).
true
9> git:status_changed_files(Local).
[{untracked,"./new_file"}]
10> os:cmd("echo >> "++Local++"/README.md").
[]
11> git:status_changed_files(Local).
[{modified,"./README.md"},{untracked,"./new_file"}]
12> git:add_files(Local, ["new_file"]).
{ok,[]}
13> git:status_changed_files(Local).
[{modified,"./README.md"},{indexed_added,"./new_file"}]
14> git:commit(Local, "update README and add file").
{ok,"[master 3825b3c] update README and add file\n 0 files changed\n create mode 100644 new_file\n"}
15> git:head(Local).
"3825b3cb5e713c5145b4b74445a4d5e6187e567d"
```

Author
======
Gleb Peregud <gleber.p@gmail.com> for LivePress Inc.

Copyright 2011-2012 LivePress Inc.

License
=======

MIT license
