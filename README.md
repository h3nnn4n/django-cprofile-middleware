# django-cprofile-middleware

This is a fork of omarish's
[django-cprofile-middleware](https://github.com/omarish/django-cprofile-middleware/).
The original project is abandoned and needs some work in order to keep it
usable. It is an awesome lib and this fork aims at keep it running.

## Installing

```bash
$ pip install git+https://github.com/h3nnn4n/django-cprofile-middleware@v1.1.0
```

Then add
`django_cprofile_middleware.middleware.ProfilerMiddleware`
to the end your `MIDDLEWARE` in `settings.py`.  This option was called
`MIDDLEWARE_CLASSES` in versions of Django before
[1.10](https://docs.djangoproject.com/en/1.10/topics/http/middleware/).

For example:

```python
MIDDLEWARE_CLASSES = (
    "django.middleware.common.CommonMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "startup.do.work.FindProductMarketFitMiddleware",
    "etc",
    "django_cprofile_middleware.middleware.ProfilerMiddleware",
)
```

The profiler will only be available when the Django setting `DEBUG` is set to
`True`. By default it's also required to be an authenticated user with
`is_staff` set to `True` which is making the request to be profiled. The
`is_staff` check can be configured as follows:

```python
DJANGO_CPROFILE_MIDDLEWARE_REQUIRE_STAFF = False
```

## Running & Sorting Results

Once you've installed it, log in as a user who has staff privileges and add
`?prof` to any URL to see the profiler's stats. For example to see profile
stats for `http://localhost:8000/foo/`, visit
`http://localhost:8000/foo/?prof`.

You can also pass some options:

**count:** The number of results you'd like to see. Default is 100.

**sort:** The field you'd like to sort results by. Default is `time`. For
all the options you can pass, see the
[docs for pstats](http://docs.python.org/2/library/profile.html#pstats.Stats.sort_stats).

**download:** Download profile file, that can be visualized in multiple
viewers, e.g. [SnakeViz](https://github.com/jiffyclub/snakeviz/) or
[RunSnakeRun](http://www.vrplumber.com/programming/runsnakerun/)

## Testing

To run unit tests it is necessary to have django available. You can do `python
-m pip install django==1.11` for example, to test with a specific version of
it. Ideally a virtual env or similar should be setup.

With django setup, the tests can be run with
```
python -m unittest
```

# LICENSE

The code is released under MIT license. See [LICENSE](LICENSE.txt) for more
details.
