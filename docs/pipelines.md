flask -e environment run --cert=adhoc
Usage: flask run [OPTIONS]
Try 'flask run --help' for help.

Error: While importing 'app', an ImportError was raised:

Traceback (most recent call last):
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask/cli.py", line 245, in locate_app
    __import__(module_name)
    ~~~~~~~~~~^^^^^^^^^^^^^
  File "/home/gtrivedi/Documents/GitLab/opl-ui/app.py", line 3, in <module>
    from flask_sqlalchemy import SQLAlchemy
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask_sqlalchemy/__init__.py", line 14, in <module>
    from flask import _app_ctx_stack, abort, current_app, request
ImportError: cannot import name '_app_ctx_stack' from 'flask' (/home/gtrivedi/.local/lib/python3.13/site-packages/flask/__init__.py)
