sudo dnf install libxml2-devel libxslt-devel
[sudo] password for gtrivedi: 
Updating and loading repositories:
Repositories loaded.
Package "libxml2-devel-2.12.9-1.fc41.x86_64" is already installed.
Package "libxslt-devel-1.1.42-2.fc41.x86_64" is already installed.

Nothing to do.
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/opl-ui$ pip install lxml
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: lxml in /usr/lib64/python3.13/site-packages (5.2.1)
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/opl-ui$ pip show lxml
Name: lxml
Version: 5.2.1
Summary: Powerful and Pythonic XML processing library combining libxml2/libxslt with the ElementTree API.
Home-page: https://lxml.de/
Author: lxml dev team
Author-email: lxml-dev@lxml.de
License: BSD-3-Clause
Location: /usr/lib64/python3.13/site-packages
Requires: 
Required-by: duplicity, redshift-connector
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/opl-ui$ flask -e environment run --cert=adhoc
Traceback (most recent call last):
  File "/home/gtrivedi/.local/bin/flask", line 8, in <module>
    sys.exit(main())
             ~~~~^^
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask/cli.py", line 1129, in main
    cli.main()
    ~~~~~~~~^^
  File "/usr/lib/python3.13/site-packages/click/core.py", line 1078, in main
    rv = self.invoke(ctx)
  File "/usr/lib/python3.13/site-packages/click/core.py", line 1688, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
                           ~~~~~~~~~~~~~~~~~~~~~~^^^^^^^^^
  File "/usr/lib/python3.13/site-packages/click/core.py", line 1434, in invoke
    return ctx.invoke(self.callback, **ctx.params)
           ~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.13/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/usr/lib/python3.13/site-packages/click/decorators.py", line 92, in new_func
    return ctx.invoke(f, obj, *args, **kwargs)
           ~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/lib/python3.13/site-packages/click/core.py", line 783, in invoke
    return __callback(*args, **kwargs)
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask/cli.py", line 977, in run_command
    raise e from None
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask/cli.py", line 961, in run_command
    app: WSGIApplication = info.load_app()  # pyright: ignore
                           ~~~~~~~~~~~~~^^
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask/cli.py", line 353, in load_app
    app = locate_app(import_name, None, raise_if_not_found=False)
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask/cli.py", line 245, in locate_app
    __import__(module_name)
    ~~~~~~~~~~^^^^^^^^^^^^^
  File "/home/gtrivedi/Documents/GitLab/opl-ui/app.py", line 3, in <module>
    from flask_sqlalchemy import SQLAlchemy
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask_sqlalchemy/__init__.py", line 5, in <module>
    from .extension import SQLAlchemy
  File "/home/gtrivedi/.local/lib/python3.13/site-packages/flask_sqlalchemy/extension.py", line 40, in <module>
    t.Type[sa_orm.DeclarativeBase],
           ^^^^^^^^^^^^^^^^^^^^^^
AttributeError: module 'sqlalchemy.orm' has no attribute 'DeclarativeBase'. Did you mean: 'declarative_base'?
gtrivedi@gtrivedi-thinkpadp16vgen1:~/Documents/GitLab/opl-ui$ pip install -r requirements.txt
Defaulting to user installation because normal site-packages is not writeable
Collecting Flask==2.3.2 (from -r requirements.txt (line 1))
  Using cached Flask-2.3.2-py3-none-any.whl.metadata (3.7 kB)
Collecting Werkzeug==2.3.8 (from -r requirements.txt (line 2))
  Using cached werkzeug-2.3.8-py3-none-any.whl.metadata (4.1 kB)
Collecting SQLAlchemy==1.4.52 (from -r requirements.txt (line 3))
  Using cached SQLAlchemy-1.4.52-cp313-cp313-linux_x86_64.whl
Collecting Flask-SQLAlchemy==3.0.3 (from -r requirements.txt (line 4))
  Using cached Flask_SQLAlchemy-3.0.3-py3-none-any.whl.metadata (3.4 kB)
Collecting Flask-WTF==1.1.1 (from -r requirements.txt (line 5))
  Using cached Flask_WTF-1.1.1-py3-none-any.whl.metadata (1.9 kB)
Collecting WTForms==3.1.1 (from -r requirements.txt (line 6))
  Using cached wtforms-3.1.1-py3-none-any.whl.metadata (5.3 kB)
Collecting WTForms-SQLAlchemy==0.3 (from -r requirements.txt (line 7))
  Using cached WTForms_SQLAlchemy-0.3-py3-none-any.whl.metadata (2.7 kB)
Requirement already satisfied: PyYAML==6.0.1 in /usr/lib64/python3.13/site-packages (from -r requirements.txt (line 8)) (6.0.1)
Collecting db-sqlite3==0.0.1 (from -r requirements.txt (line 9))
  Using cached db_sqlite3-0.0.1-py3-none-any.whl
Collecting python-math==0.0.1 (from -r requirements.txt (line 10))
  Using cached python_math-0.0.1-py3-none-any.whl.metadata (647 bytes)
Collecting click==8.1.3 (from -r requirements.txt (line 11))
  Using cached click-8.1.3-py3-none-any.whl.metadata (3.2 kB)
Collecting uuid==1.30 (from -r requirements.txt (line 12))
  Using cached uuid-1.30-py3-none-any.whl
Collecting psycopg2==2.9.6 (from -r requirements.txt (line 13))
  Using cached psycopg2-2.9.6.tar.gz (383 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Requirement already satisfied: flask_saml==0.5.1 in /home/gtrivedi/.local/lib/python3.13/site-packages (from -r requirements.txt (line 14)) (0.5.1)
Requirement already satisfied: flask_principal==0.4.0 in /home/gtrivedi/.local/lib/python3.13/site-packages (from -r requirements.txt (line 15)) (0.4.0)
Collecting pyOpenSSL==24.1.0 (from -r requirements.txt (line 16))
  Using cached pyOpenSSL-24.1.0-py3-none-any.whl.metadata (12 kB)
Collecting cryptography==42.0.8 (from -r requirements.txt (line 17))
  Using cached cryptography-42.0.8-cp39-abi3-manylinux_2_28_x86_64.whl.metadata (5.3 kB)
Collecting lxml==4.9.3 (from -r requirements.txt (line 18))
  Using cached lxml-4.9.3.tar.gz (3.6 MB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting gunicorn==20.1.0 (from -r requirements.txt (line 19))
  Using cached gunicorn-20.1.0-py3-none-any.whl.metadata (3.8 kB)
Collecting redshift_connector==2.0.909 (from -r requirements.txt (line 20))
  Using cached redshift_connector-2.0.909-py3-none-any.whl.metadata (61 kB)
Collecting sqlalchemy-redshift==0.8.13 (from -r requirements.txt (line 21))
  Using cached sqlalchemy_redshift-0.8.13-py2.py3-none-any.whl.metadata (18 kB)
Collecting urllib3==1.26.18 (from -r requirements.txt (line 22))
  Using cached urllib3-1.26.18-py2.py3-none-any.whl.metadata (48 kB)
Collecting requests==2.31.0 (from -r requirements.txt (line 23))
  Using cached requests-2.31.0-py3-none-any.whl.metadata (4.6 kB)
Requirement already satisfied: apscheduler>=3.9.1 in /home/gtrivedi/.local/lib/python3.13/site-packages (from -r requirements.txt (line 24)) (3.11.0)
Requirement already satisfied: Jinja2>=3.1.2 in /usr/lib/python3.13/site-packages (from Flask==2.3.2->-r requirements.txt (line 1)) (3.1.5)
Requirement already satisfied: itsdangerous>=2.1.2 in /home/gtrivedi/.local/lib/python3.13/site-packages (from Flask==2.3.2->-r requirements.txt (line 1)) (2.2.0)
Requirement already satisfied: blinker>=1.6.2 in /home/gtrivedi/.local/lib/python3.13/site-packages (from Flask==2.3.2->-r requirements.txt (line 1)) (1.9.0)
Requirement already satisfied: MarkupSafe>=2.1.1 in /usr/lib64/python3.13/site-packages (from Werkzeug==2.3.8->-r requirements.txt (line 2)) (2.1.5)
Requirement already satisfied: greenlet!=0.4.17 in /home/gtrivedi/.local/lib/python3.13/site-packages (from SQLAlchemy==1.4.52->-r requirements.txt (line 3)) (3.1.1)
Collecting db (from db-sqlite3==0.0.1->-r requirements.txt (line 9))
  Using cached db-0.1.1-py3-none-any.whl
Requirement already satisfied: pysaml2>=6.5.0 in /home/gtrivedi/.local/lib/python3.13/site-packages (from flask_saml==0.5.1->-r requirements.txt (line 14)) (7.5.0)
Requirement already satisfied: cffi>=1.12 in /usr/lib64/python3.13/site-packages (from cryptography==42.0.8->-r requirements.txt (line 17)) (1.17.0)
Requirement already satisfied: setuptools>=3.0 in /usr/lib/python3.13/site-packages (from gunicorn==20.1.0->-r requirements.txt (line 19)) (69.2.0)
Requirement already satisfied: scramp<1.5.0,>=1.2.0 in /home/gtrivedi/.local/lib/python3.13/site-packages (from redshift_connector==2.0.909->-r requirements.txt (line 20)) (1.4.5)
Requirement already satisfied: pytz>=2020.1 in /usr/lib/python3.13/site-packages (from redshift_connector==2.0.909->-r requirements.txt (line 20)) (2024.2)
Requirement already satisfied: beautifulsoup4<5.0.0,>=4.7.0 in /usr/lib/python3.13/site-packages (from redshift_connector==2.0.909->-r requirements.txt (line 20)) (4.12.3)
Requirement already satisfied: boto3<2.0.0,>=1.9.201 in /usr/lib/python3.13/site-packages (from redshift_connector==2.0.909->-r requirements.txt (line 20)) (1.35.93)
Requirement already satisfied: botocore<2.0.0,>=1.12.201 in /usr/lib/python3.13/site-packages (from redshift_connector==2.0.909->-r requirements.txt (line 20)) (1.35.93)
Requirement already satisfied: packaging in /usr/lib/python3.13/site-packages (from redshift_connector==2.0.909->-r requirements.txt (line 20)) (24.1)
Requirement already satisfied: charset-normalizer<4,>=2 in /usr/lib/python3.13/site-packages (from requests==2.31.0->-r requirements.txt (line 23)) (3.3.2)
Requirement already satisfied: idna<4,>=2.5 in /usr/lib/python3.13/site-packages (from requests==2.31.0->-r requirements.txt (line 23)) (3.7)
Collecting certifi>=2017.4.17 (from requests==2.31.0->-r requirements.txt (line 23))
  Using cached certifi-2024.12.14-py3-none-any.whl.metadata (2.3 kB)
Requirement already satisfied: tzlocal>=3.0 in /home/gtrivedi/.local/lib/python3.13/site-packages (from apscheduler>=3.9.1->-r requirements.txt (line 24)) (5.2)
Requirement already satisfied: soupsieve>1.2 in /usr/lib/python3.13/site-packages (from beautifulsoup4<5.0.0,>=4.7.0->redshift_connector==2.0.909->-r requirements.txt (line 20)) (2.6)
Requirement already satisfied: jmespath<2.0.0,>=0.7.1 in /usr/lib/python3.13/site-packages (from boto3<2.0.0,>=1.9.201->redshift_connector==2.0.909->-r requirements.txt (line 20)) (1.0.1)
Requirement already satisfied: s3transfer<0.11.0,>=0.10.0 in /usr/lib/python3.13/site-packages (from boto3<2.0.0,>=1.9.201->redshift_connector==2.0.909->-r requirements.txt (line 20)) (0.10.4)
Requirement already satisfied: python-dateutil<3.0.0,>=2.1 in /usr/lib/python3.13/site-packages (from botocore<2.0.0,>=1.12.201->redshift_connector==2.0.909->-r requirements.txt (line 20)) (2.8.2)
Requirement already satisfied: pycparser in /usr/lib/python3.13/site-packages (from cffi>=1.12->cryptography==42.0.8->-r requirements.txt (line 17)) (2.20)
Requirement already satisfied: defusedxml in /home/gtrivedi/.local/lib/python3.13/site-packages (from pysaml2>=6.5.0->flask_saml==0.5.1->-r requirements.txt (line 14)) (0.7.1)
Requirement already satisfied: xmlschema<3,>=2 in /home/gtrivedi/.local/lib/python3.13/site-packages (from pysaml2>=6.5.0->flask_saml==0.5.1->-r requirements.txt (line 14)) (2.5.1)
Requirement already satisfied: asn1crypto>=1.5.1 in /home/gtrivedi/.local/lib/python3.13/site-packages (from scramp<1.5.0,>=1.2.0->redshift_connector==2.0.909->-r requirements.txt (line 20)) (1.5.1)
Collecting antiorm (from db->db-sqlite3==0.0.1->-r requirements.txt (line 9))
  Using cached antiorm-1.2.1-py3-none-any.whl
Requirement already satisfied: six>=1.5 in /usr/lib/python3.13/site-packages (from python-dateutil<3.0.0,>=2.1->botocore<2.0.0,>=1.12.201->redshift_connector==2.0.909->-r requirements.txt (line 20)) (1.16.0)
Requirement already satisfied: elementpath<5.0.0,>=4.1.5 in /home/gtrivedi/.local/lib/python3.13/site-packages (from xmlschema<3,>=2->pysaml2>=6.5.0->flask_saml==0.5.1->-r requirements.txt (line 14)) (4.7.0)
Requirement already satisfied: ply==3.11 in /usr/lib/python3.13/site-packages (from pycparser->cffi>=1.12->cryptography==42.0.8->-r requirements.txt (line 17)) (3.11)
Using cached Flask-2.3.2-py3-none-any.whl (96 kB)
Using cached werkzeug-2.3.8-py3-none-any.whl (242 kB)
Using cached Flask_SQLAlchemy-3.0.3-py3-none-any.whl (24 kB)
Using cached Flask_WTF-1.1.1-py3-none-any.whl (12 kB)
Using cached wtforms-3.1.1-py3-none-any.whl (145 kB)
Using cached WTForms_SQLAlchemy-0.3-py3-none-any.whl (8.8 kB)
Using cached python_math-0.0.1-py3-none-any.whl (2.4 kB)
Using cached click-8.1.3-py3-none-any.whl (96 kB)
Using cached pyOpenSSL-24.1.0-py3-none-any.whl (56 kB)
Using cached cryptography-42.0.8-cp39-abi3-manylinux_2_28_x86_64.whl (3.9 MB)
Using cached gunicorn-20.1.0-py3-none-any.whl (79 kB)
Using cached redshift_connector-2.0.909-py3-none-any.whl (112 kB)
Using cached sqlalchemy_redshift-0.8.13-py2.py3-none-any.whl (38 kB)
Using cached urllib3-1.26.18-py2.py3-none-any.whl (143 kB)
Using cached requests-2.31.0-py3-none-any.whl (62 kB)
Using cached certifi-2024.12.14-py3-none-any.whl (164 kB)
Building wheels for collected packages: psycopg2, lxml
  Building wheel for psycopg2 (pyproject.toml) ... error
  error: subprocess-exited-with-error
  
  × Building wheel for psycopg2 (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [102 lines of output]
      running bdist_wheel
      running build
      running build_py
      creating build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/__init__.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/_ipaddress.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/_json.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/_range.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/errorcodes.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/errors.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/extensions.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/extras.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/pool.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/sql.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      copying lib/tz.py -> build/lib.linux-x86_64-cpython-313/psycopg2
      running build_ext
      building 'psycopg2._psycopg' extension
      creating build/temp.linux-x86_64-cpython-313/psycopg
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_asis.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_asis.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_binary.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_binary.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_datetime.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_datetime.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_list.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_list.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_pboolean.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_pboolean.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_pdecimal.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_pdecimal.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_pfloat.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_pfloat.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_pint.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_pint.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/adapter_qstring.c -o build/temp.linux-x86_64-cpython-313/psycopg/adapter_qstring.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/aix_support.c -o build/temp.linux-x86_64-cpython-313/psycopg/aix_support.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/bytes_format.c -o build/temp.linux-x86_64-cpython-313/psycopg/bytes_format.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/column_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/column_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/connection_int.c -o build/temp.linux-x86_64-cpython-313/psycopg/connection_int.o -Wdeclaration-after-statement
      psycopg/connection_int.c: In function ‘_conn_get_async_cursor’:
      psycopg/connection_int.c:1050:5: warning: ‘PyWeakref_GetObject’ is deprecated [-Wdeprecated-declarations]
       1050 |     if (!(py_curs = PyWeakref_GetObject(self->async_cursor))) {
            |     ^~
      In file included from /usr/include/python3.13/Python.h:113,
                       from ./psycopg/psycopg.h:35,
                       from psycopg/connection_int.c:28:
      /usr/include/python3.13/weakrefobject.h:30:44: note: declared here
         30 | Py_DEPRECATED(3.13) PyAPI_FUNC(PyObject *) PyWeakref_GetObject(PyObject *ref);
            |                                            ^~~~~~~~~~~~~~~~~~~
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/connection_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/connection_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/conninfo_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/conninfo_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/cursor_int.c -o build/temp.linux-x86_64-cpython-313/psycopg/cursor_int.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/cursor_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/cursor_type.o -Wdeclaration-after-statement
      psycopg/cursor_type.c: In function ‘curs_fetchone’:
      psycopg/cursor_type.c:782:9: warning: ‘PyWeakref_GetObject’ is deprecated [-Wdeprecated-declarations]
        782 |         && PyWeakref_GetObject(self->conn->async_cursor) == (PyObject*)self)
            |         ^~
      In file included from /usr/include/python3.13/Python.h:113,
                       from ./psycopg/psycopg.h:35,
                       from psycopg/cursor_type.c:28:
      /usr/include/python3.13/weakrefobject.h:30:44: note: declared here
         30 | Py_DEPRECATED(3.13) PyAPI_FUNC(PyObject *) PyWeakref_GetObject(PyObject *ref);
            |                                            ^~~~~~~~~~~~~~~~~~~
      psycopg/cursor_type.c: In function ‘curs_next_named’:
      psycopg/cursor_type.c:829:9: warning: ‘PyWeakref_GetObject’ is deprecated [-Wdeprecated-declarations]
        829 |         && PyWeakref_GetObject(self->conn->async_cursor) == (PyObject*)self)
            |         ^~
      /usr/include/python3.13/weakrefobject.h:30:44: note: declared here
         30 | Py_DEPRECATED(3.13) PyAPI_FUNC(PyObject *) PyWeakref_GetObject(PyObject *ref);
            |                                            ^~~~~~~~~~~~~~~~~~~
      psycopg/cursor_type.c: In function ‘curs_fetchmany’:
      psycopg/cursor_type.c:914:9: warning: ‘PyWeakref_GetObject’ is deprecated [-Wdeprecated-declarations]
        914 |         && PyWeakref_GetObject(self->conn->async_cursor) == (PyObject*)self)
            |         ^~
      /usr/include/python3.13/weakrefobject.h:30:44: note: declared here
         30 | Py_DEPRECATED(3.13) PyAPI_FUNC(PyObject *) PyWeakref_GetObject(PyObject *ref);
            |                                            ^~~~~~~~~~~~~~~~~~~
      psycopg/cursor_type.c: In function ‘curs_fetchall’:
      psycopg/cursor_type.c:983:9: warning: ‘PyWeakref_GetObject’ is deprecated [-Wdeprecated-declarations]
        983 |         && PyWeakref_GetObject(self->conn->async_cursor) == (PyObject*)self)
            |         ^~
      /usr/include/python3.13/weakrefobject.h:30:44: note: declared here
         30 | Py_DEPRECATED(3.13) PyAPI_FUNC(PyObject *) PyWeakref_GetObject(PyObject *ref);
            |                                            ^~~~~~~~~~~~~~~~~~~
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/diagnostics_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/diagnostics_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/error_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/error_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/green.c -o build/temp.linux-x86_64-cpython-313/psycopg/green.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/libpq_support.c -o build/temp.linux-x86_64-cpython-313/psycopg/libpq_support.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/lobject_int.c -o build/temp.linux-x86_64-cpython-313/psycopg/lobject_int.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/lobject_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/lobject_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/microprotocols.c -o build/temp.linux-x86_64-cpython-313/psycopg/microprotocols.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/microprotocols_proto.c -o build/temp.linux-x86_64-cpython-313/psycopg/microprotocols_proto.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/notify_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/notify_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/pqpath.c -o build/temp.linux-x86_64-cpython-313/psycopg/pqpath.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/psycopgmodule.c -o build/temp.linux-x86_64-cpython-313/psycopg/psycopgmodule.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/replication_connection_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/replication_connection_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/replication_cursor_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/replication_cursor_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/replication_message_type.c -o build/temp.linux-x86_64-cpython-313/psycopg/replication_message_type.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/solaris_support.c -o build/temp.linux-x86_64-cpython-313/psycopg/solaris_support.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/typecast.c -o build/temp.linux-x86_64-cpython-313/psycopg/typecast.o -Wdeclaration-after-statement
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC "-DPSYCOPG_VERSION=2.9.6 (dt dec pq3 ext lo64)" -DPSYCOPG_DEBUG=1 -DPG_VERSION_NUM=160004 -DHAVE_LO64=1 -DPSYCOPG_DEBUG=1 -I/usr/include/python3.13 -I. -I/usr/include -I/usr/include/pgsql/server -c psycopg/utils.c -o build/temp.linux-x86_64-cpython-313/psycopg/utils.o -Wdeclaration-after-statement
      psycopg/utils.c: In function ‘psyco_is_main_interp’:
      psycopg/utils.c:397:12: error: implicit declaration of function ‘_PyInterpreterState_Get’; did you mean ‘PyInterpreterState_Get’? [-Wimplicit-function-declaration]
        397 |     return _PyInterpreterState_Get() == PyInterpreterState_Main();
            |            ^~~~~~~~~~~~~~~~~~~~~~~
            |            PyInterpreterState_Get
      psycopg/utils.c:397:38: warning: comparison between pointer and integer
        397 |     return _PyInterpreterState_Get() == PyInterpreterState_Main();
            |                                      ^~
      error: command '/usr/bin/gcc' failed with exit code 1
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for psycopg2
  Building wheel for lxml (pyproject.toml) ... error
  error: subprocess-exited-with-error
  
  × Building wheel for lxml (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [344 lines of output]
      <string>:67: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
      Building lxml version 4.9.3.
      Building without Cython.
      Building against libxml2 2.12.9 and libxslt 1.1.42
      running bdist_wheel
      running build
      running build_py
      creating build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/ElementInclude.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/__init__.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/_elementpath.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/builder.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/cssselect.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/doctestcompare.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/pyclasslookup.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/sax.py -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/usedoctest.py -> build/lib.linux-x86_64-cpython-313/lxml
      creating build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/__init__.py -> build/lib.linux-x86_64-cpython-313/lxml/includes
      creating build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/ElementSoup.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/__init__.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/_diffcommand.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/_html5builder.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/_setmixin.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/builder.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/clean.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/defs.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/diff.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/formfill.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/html5parser.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/soupparser.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      copying src/lxml/html/usedoctest.py -> build/lib.linux-x86_64-cpython-313/lxml/html
      creating build/lib.linux-x86_64-cpython-313/lxml/isoschematron
      copying src/lxml/isoschematron/__init__.py -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron
      copying src/lxml/etree.h -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/etree_api.h -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/lxml.etree.h -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/lxml.etree_api.h -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/etree.pyx -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/objectify.pyx -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/apihelpers.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/classlookup.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/cleanup.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/debug.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/docloader.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/dtd.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/extensions.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/iterparse.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/nsclasses.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/objectpath.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/parser.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/parsertarget.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/proxy.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/public-api.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/readonlytree.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/relaxng.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/saxparser.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/schematron.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/serializer.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xinclude.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xmlerror.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xmlid.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xmlschema.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xpath.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xslt.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/xsltext.pxi -> build/lib.linux-x86_64-cpython-313/lxml
      copying src/lxml/includes/__init__.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/c14n.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/config.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/dtdvalid.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/etreepublic.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/htmlparser.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/relaxng.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/schematron.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/tree.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/uri.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/xinclude.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/xmlerror.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/xmlparser.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/xmlschema.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/xpath.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/xslt.pxd -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/etree_defs.h -> build/lib.linux-x86_64-cpython-313/lxml/includes
      copying src/lxml/includes/lxml-version.h -> build/lib.linux-x86_64-cpython-313/lxml/includes
      creating build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/rng
      copying src/lxml/isoschematron/resources/rng/iso-schematron.rng -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/rng
      creating build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl
      copying src/lxml/isoschematron/resources/xsl/RNG2Schtrn.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl
      copying src/lxml/isoschematron/resources/xsl/XSD2Schtrn.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl
      creating build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      copying src/lxml/isoschematron/resources/xsl/iso-schematron-xslt1/iso_abstract_expand.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      copying src/lxml/isoschematron/resources/xsl/iso-schematron-xslt1/iso_dsdl_include.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      copying src/lxml/isoschematron/resources/xsl/iso-schematron-xslt1/iso_schematron_message.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      copying src/lxml/isoschematron/resources/xsl/iso-schematron-xslt1/iso_schematron_skeleton_for_xslt1.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      copying src/lxml/isoschematron/resources/xsl/iso-schematron-xslt1/iso_svrl_for_xslt1.xsl -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      copying src/lxml/isoschematron/resources/xsl/iso-schematron-xslt1/readme.txt -> build/lib.linux-x86_64-cpython-313/lxml/isoschematron/resources/xsl/iso-schematron-xslt1
      running build_ext
      building 'lxml.etree' extension
      creating build/temp.linux-x86_64-cpython-313/src/lxml
      gcc -fno-strict-overflow -Wsign-compare -DDYNAMIC_ANNOTATIONS_ENABLED=1 -DNDEBUG -fcf-protection -fexceptions -fcf-protection -fexceptions -fcf-protection -fexceptions -O3 -fPIC -DCYTHON_CLINE_IN_TRACEBACK=0 -I/usr/include/libxml2 -Isrc -Isrc/lxml/includes -I/usr/include/python3.13 -c src/lxml/etree.c -o build/temp.linux-x86_64-cpython-313/src/lxml/etree.o -w -DWITH_GZFILEOP
      src/lxml/etree.c: In function ‘__Pyx_init_assertions_enabled’:
      src/lxml/etree.c:5988:39: error: implicit declaration of function ‘_PyInterpreterState_GetConfig’; did you mean ‘PyInterpreterState_GetID’? [-Wimplicit-function-declaration]
       5988 |     __pyx_assertions_enabled_flag = ! _PyInterpreterState_GetConfig(__Pyx_PyThreadState_Current->interp)->optimization_level;
            |                                       ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            |                                       PyInterpreterState_GetID
      src/lxml/etree.c:5988:105: error: invalid type argument of ‘->’ (have ‘int’)
       5988 |     __pyx_assertions_enabled_flag = ! _PyInterpreterState_GetConfig(__Pyx_PyThreadState_Current->interp)->optimization_level;
            |                                                                                                         ^~
      src/lxml/etree.c: In function ‘__pyx_f_4lxml_5etree_14_ParserContext_prepare’:
      src/lxml/etree.c:113152:38: error: assignment to ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} from incompatible pointer type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’} [-Wincompatible-pointer-types]
      113152 |   __pyx_v_self->_c_ctxt->sax->serror = __pyx_f_4lxml_5etree__receiveParserError;
             |                                      ^
      src/lxml/etree.c: In function ‘__pyx_f_4lxml_5etree_11_BaseParser__registerHtmlErrorHandler’:
      src/lxml/etree.c:117640:25: error: assignment to ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} from incompatible pointer type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’} [-Wincompatible-pointer-types]
      117640 |     __pyx_v_sax->serror = __pyx_f_4lxml_5etree__receiveParserError;
             |                         ^
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_11TreeBuilder_4data’:
      src/lxml/etree.c:137729:66: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxData’ from incompatible pointer type [-Wincompatible-pointer-types]
      137729 |   __pyx_t_1 = __pyx_f_4lxml_5etree_11TreeBuilder__handleSaxData(((struct __pyx_obj_4lxml_5etree__SaxParserTarget *)__pyx_v_self), __pyx_v_data); if (unlikely(__pyx_t_1 == ((int)-1))) __PYX_ERR(3, 832, __pyx_L1_error)
             |                                                                 ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                  |
             |                                                                  struct __pyx_obj_4lxml_5etree__SaxParserTarget *
      src/lxml/etree.c:137105:105: note: expected ‘struct __pyx_obj_4lxml_5etree_TreeBuilder *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__SaxParserTarget *’
      137105 | static int __pyx_f_4lxml_5etree_11TreeBuilder__handleSaxData(struct __pyx_obj_4lxml_5etree_TreeBuilder *__pyx_v_self, PyObject *__pyx_v_data) {
             |                                                              ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_11TreeBuilder_6start’:
      src/lxml/etree.c:137890:67: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxStart’ from incompatible pointer type [-Wincompatible-pointer-types]
      137890 |   __pyx_t_3 = __pyx_f_4lxml_5etree_11TreeBuilder__handleSaxStart(((struct __pyx_obj_4lxml_5etree__SaxParserTarget *)__pyx_v_self), __pyx_v_tag, __pyx_v_attrs, __pyx_v_nsmap); if (unlikely(!__pyx_t_3)) __PYX_ERR(3, 841, __pyx_L1_error)
             |                                                                  ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                   |
             |                                                                   struct __pyx_obj_4lxml_5etree__SaxParserTarget *
      src/lxml/etree.c:136704:112: note: expected ‘struct __pyx_obj_4lxml_5etree_TreeBuilder *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__SaxParserTarget *’
      136704 | static PyObject *__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxStart(struct __pyx_obj_4lxml_5etree_TreeBuilder *__pyx_v_self, PyObject *__pyx_v_tag, PyObject *__pyx_v_attrib, PyObject *__pyx_v_nsmap) {
             |                                                                     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_11TreeBuilder_8end’:
      src/lxml/etree.c:137961:65: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxEnd’ from incompatible pointer type [-Wincompatible-pointer-types]
      137961 |   __pyx_t_1 = __pyx_f_4lxml_5etree_11TreeBuilder__handleSaxEnd(((struct __pyx_obj_4lxml_5etree__SaxParserTarget *)__pyx_v_self), __pyx_v_tag); if (unlikely(!__pyx_t_1)) __PYX_ERR(3, 848, __pyx_L1_error)
             |                                                                ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                 |
             |                                                                 struct __pyx_obj_4lxml_5etree__SaxParserTarget *
      src/lxml/etree.c:137004:110: note: expected ‘struct __pyx_obj_4lxml_5etree_TreeBuilder *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__SaxParserTarget *’
      137004 | static PyObject *__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxEnd(struct __pyx_obj_4lxml_5etree_TreeBuilder *__pyx_v_self, CYTHON_UNUSED PyObject *__pyx_v_tag) {
             |                                                                   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_11TreeBuilder_10pi’:
      src/lxml/etree.c:138162:64: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxPi’ from incompatible pointer type [-Wincompatible-pointer-types]
      138162 |   __pyx_t_1 = __pyx_f_4lxml_5etree_11TreeBuilder__handleSaxPi(((struct __pyx_obj_4lxml_5etree__SaxParserTarget *)__pyx_v_self), __pyx_v_target, __pyx_v_data); if (unlikely(!__pyx_t_1)) __PYX_ERR(3, 859, __pyx_L1_error)
             |                                                               ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                |
             |                                                                struct __pyx_obj_4lxml_5etree__SaxParserTarget *
      src/lxml/etree.c:137154:109: note: expected ‘struct __pyx_obj_4lxml_5etree_TreeBuilder *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__SaxParserTarget *’
      137154 | static PyObject *__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxPi(struct __pyx_obj_4lxml_5etree_TreeBuilder *__pyx_v_self, PyObject *__pyx_v_target, PyObject *__pyx_v_data) {
             |                                                                  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_11TreeBuilder_12comment’:
      src/lxml/etree.c:138225:69: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxComment’ from incompatible pointer type [-Wincompatible-pointer-types]
      138225 |   __pyx_t_1 = __pyx_f_4lxml_5etree_11TreeBuilder__handleSaxComment(((struct __pyx_obj_4lxml_5etree__SaxParserTarget *)__pyx_v_self), __pyx_v_comment); if (unlikely(!__pyx_t_1)) __PYX_ERR(3, 867, __pyx_L1_error)
             |                                                                    ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                     |
             |                                                                     struct __pyx_obj_4lxml_5etree__SaxParserTarget *
      src/lxml/etree.c:137360:114: note: expected ‘struct __pyx_obj_4lxml_5etree_TreeBuilder *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__SaxParserTarget *’
      137360 | static PyObject *__pyx_f_4lxml_5etree_11TreeBuilder__handleSaxComment(struct __pyx_obj_4lxml_5etree_TreeBuilder *__pyx_v_self, PyObject *__pyx_v_comment) {
             |                                                                       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_f_4lxml_5etree_12_BaseContext__set_xpath_context’:
      src/lxml/etree.c:181724:28: error: assignment to ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} from incompatible pointer type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’} [-Wincompatible-pointer-types]
      181724 |   __pyx_v_xpathCtxt->error = __pyx_f_4lxml_5etree__receiveXPathError;
             |                            ^
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_4XSLT_18__call__’:
      src/lxml/etree.c:203239:73: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_12_XSLTContext__copy’ from incompatible pointer type [-Wincompatible-pointer-types]
      203239 |     __pyx_t_1 = ((PyObject *)__pyx_f_4lxml_5etree_12_XSLTContext__copy(((struct __pyx_obj_4lxml_5etree__BaseContext *)__pyx_v_self->_context))); if (unlikely(!__pyx_t_1)) __PYX_ERR(4, 550, __pyx_L9_error)
             |                                                                        ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                         |
             |                                                                         struct __pyx_obj_4lxml_5etree__BaseContext *
      src/lxml/etree.c:200922:138: note: expected ‘struct __pyx_obj_4lxml_5etree__XSLTContext *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__BaseContext *’
      200922 | static struct __pyx_obj_4lxml_5etree__BaseContext *__pyx_f_4lxml_5etree_12_XSLTContext__copy(struct __pyx_obj_4lxml_5etree__XSLTContext *__pyx_v_self) {
             |                                                                                              ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_f_4lxml_5etree__copyXSLT’:
      src/lxml/etree.c:205064:71: error: passing argument 1 of ‘__pyx_f_4lxml_5etree_12_XSLTContext__copy’ from incompatible pointer type [-Wincompatible-pointer-types]
      205064 |   __pyx_t_1 = ((PyObject *)__pyx_f_4lxml_5etree_12_XSLTContext__copy(((struct __pyx_obj_4lxml_5etree__BaseContext *)__pyx_v_stylesheet->_context))); if (unlikely(!__pyx_t_1)) __PYX_ERR(4, 691, __pyx_L1_error)
             |                                                                      ~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                       |
             |                                                                       struct __pyx_obj_4lxml_5etree__BaseContext *
      src/lxml/etree.c:200922:138: note: expected ‘struct __pyx_obj_4lxml_5etree__XSLTContext *’ but argument is of type ‘struct __pyx_obj_4lxml_5etree__BaseContext *’
      200922 | static struct __pyx_obj_4lxml_5etree__BaseContext *__pyx_f_4lxml_5etree_12_XSLTContext__copy(struct __pyx_obj_4lxml_5etree__XSLTContext *__pyx_v_self) {
             |                                                                                              ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_7RelaxNG_2__init__’:
      src/lxml/etree.c:218998:60: error: passing argument 2 of ‘xmlRelaxNGSetParserStructuredErrors’ from incompatible pointer type [-Wincompatible-pointer-types]
      218998 |   xmlRelaxNGSetParserStructuredErrors(__pyx_v_parser_ctxt, __pyx_f_4lxml_5etree__receiveError, ((void *)__pyx_v_self->__pyx_base._error_log));
             |                                                            ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                            |
             |                                                            void (*)(void *, xmlError *) {aka void (*)(void *, struct _xmlError *)}
      In file included from src/lxml/etree.c:905:
      /usr/include/libxml2/libxml/relaxng.h:156:65: note: expected ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} but argument is of type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’}
        156 |                                          xmlStructuredErrorFunc serror,
            |                                          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_7RelaxNG_6__call__’:
      src/lxml/etree.c:219416:60: error: passing argument 2 of ‘xmlRelaxNGSetValidStructuredErrors’ from incompatible pointer type [-Wincompatible-pointer-types]
      219416 |     xmlRelaxNGSetValidStructuredErrors(__pyx_v_valid_ctxt, __pyx_f_4lxml_5etree__receiveError, ((void *)__pyx_v_self->__pyx_base._error_log));
             |                                                            ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                            |
             |                                                            void (*)(void *, xmlError *) {aka void (*)(void *, struct _xmlError *)}
      /usr/include/libxml2/libxml/relaxng.h:185:66: note: expected ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} but argument is of type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’}
        185 |                                           xmlStructuredErrorFunc serror, void *ctx);
            |                                           ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_9XMLSchema_2__init__’:
      src/lxml/etree.c:220305:59: error: passing argument 2 of ‘xmlSchemaSetParserStructuredErrors’ from incompatible pointer type [-Wincompatible-pointer-types]
      220305 |   xmlSchemaSetParserStructuredErrors(__pyx_v_parser_ctxt, __pyx_f_4lxml_5etree__receiveError, ((void *)__pyx_v_self->__pyx_base._error_log));
             |                                                           ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                           |
             |                                                           void (*)(void *, xmlError *) {aka void (*)(void *, struct _xmlError *)}
      In file included from src/lxml/etree.c:906:
      /usr/include/libxml2/libxml/xmlschemas.h:156:65: note: expected ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} but argument is of type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’}
        156 |                                          xmlStructuredErrorFunc serror,
            |                                          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_9XMLSchema_6__call__’:
      src/lxml/etree.c:220848:59: error: passing argument 2 of ‘xmlSchemaSetValidStructuredErrors’ from incompatible pointer type [-Wincompatible-pointer-types]
      220848 |     xmlSchemaSetValidStructuredErrors(__pyx_v_valid_ctxt, __pyx_f_4lxml_5etree__receiveError, ((void *)__pyx_v_self->__pyx_base._error_log));
             |                                                           ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                           |
             |                                                           void (*)(void *, xmlError *) {aka void (*)(void *, struct _xmlError *)}
      /usr/include/libxml2/libxml/xmlschemas.h:185:65: note: expected ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} but argument is of type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’}
        185 |                                          xmlStructuredErrorFunc serror,
            |                                          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~
      src/lxml/etree.c: In function ‘__pyx_f_4lxml_5etree_30_ParserSchemaValidationContext_connect’:
      src/lxml/etree.c:221613:66: error: passing argument 2 of ‘xmlSchemaSetValidStructuredErrors’ from incompatible pointer type [-Wincompatible-pointer-types]
      221613 |     xmlSchemaSetValidStructuredErrors(__pyx_v_self->_valid_ctxt, __pyx_f_4lxml_5etree__receiveError, ((void *)__pyx_v_error_log));
             |                                                                  ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                                  |
             |                                                                  void (*)(void *, xmlError *) {aka void (*)(void *, struct _xmlError *)}
      /usr/include/libxml2/libxml/xmlschemas.h:185:65: note: expected ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} but argument is of type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’}
        185 |                                          xmlStructuredErrorFunc serror,
            |                                          ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~
      src/lxml/etree.c: In function ‘__pyx_pf_4lxml_5etree_10Schematron_6__call__’:
      src/lxml/etree.c:222790:63: error: passing argument 2 of ‘xmlSchematronSetValidStructuredErrors’ from incompatible pointer type [-Wincompatible-pointer-types]
      222790 |     xmlSchematronSetValidStructuredErrors(__pyx_v_valid_ctxt, __pyx_f_4lxml_5etree__receiveError, ((void *)__pyx_v_self->__pyx_base._error_log));
             |                                                               ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |                                                               |
             |                                                               void (*)(void *, xmlError *) {aka void (*)(void *, struct _xmlError *)}
      In file included from src/lxml/etree.c:907:
      /usr/include/libxml2/libxml/schematron.h:106:66: note: expected ‘xmlStructuredErrorFunc’ {aka ‘void (*)(void *, const struct _xmlError *)’} but argument is of type ‘void (*)(void *, xmlError *)’ {aka ‘void (*)(void *, struct _xmlError *)’}
        106 |                                           xmlStructuredErrorFunc serror,
            |                                           ~~~~~~~~~~~~~~~~~~~~~~~^~~~~~
      src/lxml/etree.c: In function ‘__pyx_pymod_exec_etree’:
      src/lxml/etree.c:6652:38: error: implicit declaration of function ‘_PyDict_SetItem_KnownHash’; did you mean ‘_PyDict_GetItem_KnownHash’? [-Wimplicit-function-declaration]
       6652 |     (likely(PyDict_CheckExact(ns)) ? _PyDict_SetItem_KnownHash(ns, name, value, ((PyASCIIObject *) name)->hash) : PyObject_SetItem(ns, name, value))
            |                                      ^~~~~~~~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c:255116:7: note: in expansion of macro ‘__Pyx_SetNameInClass’
      255116 |   if (__Pyx_SetNameInClass(__pyx_t_2, __pyx_n_s_getitem, __pyx_t_9) < 0) __PYX_ERR(0, 97, __pyx_L1_error)
             |       ^~~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyUnicode_Join’:
      src/lxml/etree.c:264164:13: error: implicit declaration of function ‘_PyUnicode_FastCopyCharacters’; did you mean ‘PyUnicode_CopyCharacters’? [-Wimplicit-function-declaration]
      264164 |             _PyUnicode_FastCopyCharacters(result_uval, char_pos, uval, 0, ulength);
             |             ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |             PyUnicode_CopyCharacters
      src/lxml/etree.c: In function ‘__Pyx_PyIter_Next2’:
      src/lxml/etree.c:264900:35: error: ‘_PyObject_NextNotImplemented’ undeclared (first use in this function); did you mean ‘PyObject_HashNotImplemented’?
      264900 |         if (unlikely(iternext == &_PyObject_NextNotImplemented))
             |                                   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c:1096:43: note: in definition of macro ‘unlikely’
       1096 |   #define unlikely(x) __builtin_expect(!!(x), 0)
            |                                           ^
      src/lxml/etree.c:264900:35: note: each undeclared identifier is reported only once for each function it appears in
      264900 |         if (unlikely(iternext == &_PyObject_NextNotImplemented))
             |                                   ^~~~~~~~~~~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c:1096:43: note: in definition of macro ‘unlikely’
       1096 |   #define unlikely(x) __builtin_expect(!!(x), 0)
            |                                           ^
      src/lxml/etree.c: In function ‘__Pyx_PyGen_Send’:
      src/lxml/etree.c:265691:13: error: implicit declaration of function ‘_PyGen_SetStopIterationValue’; did you mean ‘__Pyx_PyGen__FetchStopIterationValue’? [-Wimplicit-function-declaration]
      265691 |             _PyGen_SetStopIterationValue(result);
             |             ^~~~~~~~~~~~~~~~~~~~~~~~~~~~
             |             __Pyx_PyGen__FetchStopIterationValue
      src/lxml/etree.c: In function ‘__Pyx_Coroutine_AwaitableIterError’:
      src/lxml/etree.c:267524:5: error: implicit declaration of function ‘_PyErr_FormatFromCause’ [-Wimplicit-function-declaration]
      267524 |     _PyErr_FormatFromCause(
             |     ^~~~~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_set_iter_next’:
      src/lxml/etree.c:267789:19: error: implicit declaration of function ‘_PySet_NextEntry’ [-Wimplicit-function-declaration]
      267789 |         int ret = _PySet_NextEntry(iter_obj, ppos, value, &hash);
             |                   ^~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_int’:
      src/lxml/etree.c:268784:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      268784 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      In file included from /usr/include/python3.13/longobject.h:107,
                       from /usr/include/python3.13/Python.h:81,
                       from src/lxml/etree.c:96:
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_size_t’:
      src/lxml/etree.c:269093:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      269093 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_unsigned_int’:
      src/lxml/etree.c:269289:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      269289 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_signed__char’:
      src/lxml/etree.c:269485:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      269485 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_unsigned_short’:
      src/lxml/etree.c:269719:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      269719 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_xmlChar’:
      src/lxml/etree.c:269953:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      269953 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      src/lxml/etree.c: In function ‘__Pyx_PyInt_As_long’:
      src/lxml/etree.c:270156:27: error: too few arguments to function ‘_PyLong_AsByteArray’
      270156 |                 int ret = _PyLong_AsByteArray((PyLongObject *)v,
             |                           ^~~~~~~~~~~~~~~~~~~
      /usr/include/python3.13/cpython/longobject.h:111:17: note: declared here
        111 | PyAPI_FUNC(int) _PyLong_AsByteArray(PyLongObject* v,
            |                 ^~~~~~~~~~~~~~~~~~~
      Compile failed: command '/usr/bin/gcc' failed with exit code 1
      creating tmp
      cc -I/usr/include/libxml2 -I/usr/include/libxml2 -c /tmp/xmlXPathInit5ck54xdp.c -o tmp/xmlXPathInit5ck54xdp.o
      /tmp/xmlXPathInit5ck54xdp.c: In function ‘main’:
      /tmp/xmlXPathInit5ck54xdp.c:3:5: warning: ‘xmlXPathInit’ is deprecated [-Wdeprecated-declarations]
          3 |     xmlXPathInit();
            |     ^~~~~~~~~~~~
      In file included from /tmp/xmlXPathInit5ck54xdp.c:1:
      /usr/include/libxml2/libxml/xpath.h:564:21: note: declared here
        564 |                     xmlXPathInit                (void);
            |                     ^~~~~~~~~~~~
      cc tmp/xmlXPathInit5ck54xdp.o -lxml2 -o a.out
      error: command '/usr/bin/gcc' failed with exit code 1
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for lxml
Failed to build psycopg2 lxml
ERROR: ERROR: Failed to build installable wheels for some pyproject.toml based projects (psycopg2, lxml)
