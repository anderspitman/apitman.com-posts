I recently started looking at libfuse. It wasn't immediately obvious to me
how to compile the examples, such as
[this one](https://github.com/libfuse/libfuse/blob/62c1941cc846aeeae04b090d5d24252ba7365a41/example/hello.c).

A naive `gcc -lib hello.c` yielded these errors:

```
In file included from /usr/include/fuse/fuse.h:26,
                 from /usr/include/fuse.h:9,
                 from hello.c:23:
/usr/include/fuse/fuse_common.h:33:2: error: #error Please add -D_FILE_OFFSET_BITS=64 to your compile flags!
   33 | #error Please add -D_FILE_OFFSET_BITS=64 to your compile flags!
      |  ^~~~~
hello.c:55:11: warning: 'struct fuse_config' declared inside parameter list will not be visible outside of this definition or declaration
   55 |    struct fuse_config *cfg)
      |           ^~~~~~~~~~~
hello.c: In function 'hello_init':
hello.c:58:5: error: dereferencing pointer to incomplete type 'struct fuse_config'
   58 |  cfg->kernel_cache = 1;
      |     ^~
hello.c: At top level:
hello.c:84:10: warning: 'enum fuse_readdir_flags' declared inside parameter list will not be visible outside of this definition or declaration
   84 |     enum fuse_readdir_flags flags)
      |          ^~~~~~~~~~~~~~~~~~
hello.c:84:29: error: parameter 6 ('flags') has incomplete type
   84 |     enum fuse_readdir_flags flags)
      |     ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~
hello.c: In function 'hello_readdir':
hello.c:93:2: error: too many arguments to function 'filler'
   93 |  filler(buf, ".", NULL, 0, 0);
      |  ^~~~~~
hello.c:94:2: error: too many arguments to function 'filler'
   94 |  filler(buf, "..", NULL, 0, 0);
      |  ^~~~~~
hello.c:95:2: error: too many arguments to function 'filler'
   95 |  filler(buf, options.filename, NULL, 0, 0);
      |  ^~~~~~
hello.c: At top level:
hello.c:131:20: warning: initialization of 'void * (*)(struct fuse_conn_info *)' from incompatible pointer type 'void * (*)(struct fuse_conn_info *, struct fuse_config *)' [-Wincompatible-pointer-types]
  131 |  .init           = hello_init,
      |                    ^~~~~~~~~~
hello.c:131:20: note: (near initialization for 'hello_oper.init')
hello.c:132:13: warning: initialization of 'int (*)(const char *, struct stat *)' from incompatible pointer type 'int (*)(const char *, struct stat *, struct fuse_file_info *)' [-Wincompatible-pointer-types]
  132 |  .getattr = hello_getattr,
      |             ^~~~~~~~~~~~~
hello.c:132:13: note: (near initialization for 'hello_oper.getattr')
```

I should have looked closer, since this line is in the file header comment:

```gcc -Wall hello.c `pkg-config fuse3 --cflags --libs` -o hello```

As you can see, you need pkg-config and libfuse installed. I had both of those,
but not the correct command.
