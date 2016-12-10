## brew

### `curl: (56) SSLRead() return error -9845`

May caused by DNS setting, try to restore your DNS setting, see more in [GitHub Issue](curl: (56) SSLRead() return error -9845)

### `Gem::Ext::BuildError: ERROR: Failed to build gem native extension....ld: library not found for -lssl`

Generally there are no consequences of this for you. If you build your own software and it requires this formula, you'll need to add to your build variables:

LDFLAGS: -L/usr/local/opt/openssl/lib
CPPFLAGS: -I/usr/local/opt/openssl/include
PKG_CONFIG_PATH: /usr/local/opt/openssl/lib/pkgconfig

You can set these build flags (for the local application) by running the following:

```shell
bundle config --local build.mysql2 "--with-ldflags=-L/usr/local/opt/openssl/lib --with-cppflags=-I/usr/local/opt/openssl/include"
```

See more in [StackOverFlow](http://stackoverflow.com/questions/30834421/error-when-trying-to-install-app-with-mysql2-gem)