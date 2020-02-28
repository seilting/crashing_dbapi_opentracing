# Crashing DBAPI-Opentracing 0.0.4 with psycopg2

This is to demonstrate a crash I am getting with Django's
`queryset.iterator()`, DBAPI-Opentracing, and psycopg2.

To replicate:

```
pip install -r requirements.txt
docker stack deploy --compose-file docker-compose.yml crashy
./crash
# Traceback (most recent call last):
#   File "./crash", line 13, in <module>
#     cur = tracing.cursor("Name", scrollable=False, withhold=True)  # crashes
#   File "/Users/simoneilting/.pyenv/versions/tracing/lib/python3.8/site-packages/dbapi_opentracing/psycopg2_tracing.py", line 115, in cursor
#     return PsycopgCursorTracing(conn=self, name=name, cursor_factory=cursor_factory, tracer=self._self_tracer,
#   File "/Users/simoneilting/.pyenv/versions/tracing/lib/python3.8/site-packages/dbapi_opentracing/psycopg2_tracing.py", line 88, in __new__
#     return _cursor_factory_classes[factory](*args, **kwargs)
#   File "/Users/simoneilting/.pyenv/versions/tracing/lib/python3.8/site-packages/dbapi_opentracing/psycopg2_tracing.py", line 83, in __init__
#     factory.__init__(self, conn, *a, **kw)
# TypeError: function takes at most 2 arguments (3 given)
```
