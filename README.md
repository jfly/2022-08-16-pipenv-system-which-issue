# pipenv system which issue

This demonstrates a bug introduced in
https://github.com/pypa/pipenv/commit/f276360dfcef3200908e2c6569567d617919c63d
(affecting pipenv v2022.3.28 - v2022.8.15) when running `pipenv install
--system` on a machine with a python3 binary but not a python binary (as is
common with many package managers, including Ubuntu's).

I've filed this issue upstream: https://github.com/pypa/pipenv/issues/5261
And this PR to fix it: https://github.com/pypa/pipenv/pull/5262

## Demonstration of the bug

    $ docker run $(docker build -q -f Dockerfile.pipenv-2022.8.15 https://github.com/jfly/2022-08-16-pipenv-system-which-issue.git#main)
    Installing dependencies from Pipfile.lock (63bec0)...
    The Python interpreter can't be found.▉ 0/4 — 00:00:00
      🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/4 — 00:00:00

## Demonstration of the fix

    $ docker run $(docker build -q -f Dockerfile.pipenv-with-fix https://github.com/jfly/2022-08-16-pipenv-system-which-issue.git#main)
    Installing dependencies from Pipfile.lock (63bec0)...
      🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 4/4 — 00:00:00
