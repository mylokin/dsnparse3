# dsnparse

[![Build Status](https://travis-ci.org/mylokin/dsnparse3.svg?branch=master)](https://travis-ci.org/mylokin/dsnparse3)

Parse [dsn connection url strings](http://en.wikipedia.org/wiki/Data_source_name). I kept duplicating dsn parsing code for things like [prom](https://github.com/firstopinion/prom) and morp, and I realized I was going to need many more dsn urls in the future so I decided to create something a little more modular.

This is a generic version of [dj-database-url](https://github.com/kennethreitz/dj-database-url).

So, now you can create dsns like this:

    scheme://user:pass@host:port/path?query=query_val#fragment

For example, let's look at a prom dsn:

    prom.interface.postgres.Interface://testuser:testpw@localhost/testdb

Now let's parse it:

```python
import dsnparse3

dsn = "prom.interface.postgres.Interface://testuser:testpw@localhost:1234/testdb"
r = dsnparse3.parse(dsn)

print r.scheme # prom.interface.postgres.Interface
print r.username # testuser
print r.password # testpw
print r.host # localhost
print r.hostloc # localhost:1234
print r.paths # ['testdb']
```

Also, dsnparse can easily use environment variables:

```python
r = dsnparse.parse_environ('ENVIRONMENT_VARIABLE_NAME')
```

## Install

Use pip:

    pip install dsnparse3

## License

MIT
