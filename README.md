NBKOJ: Nguyen Binh Khiem Online Judge
===

[![](https://github.com/DMOJ/online-judge/workflows/build/badge.svg)](http://nbk.homes)
[![Python](https://img.shields.io/pypi/pyversions/tensorflow.svg?style=plastic)](https://python.org)
[![OS](https://img.shields.io/badge/Ubuntu-16.04%20%7C%2018.04%20%7C%2020.04-brightgreen)](https://ubuntu.com/download)
[![License](https://img.shields.io/badge/license-AGPL--3.0-blue)](https://www.gnu.org/licenses/agpl-3.0.en.html)

## Overview

Homepage: [https://nbk.homes](https://nbk.homes)

Based on [DMOJ](https://dmoj.ca/) and [LQDOJ](https://lqdoj.edu.vn).

Supported languages: 

- Assembly (x64)
- AWK
- C
- C++03 / C++11 / C++14 / C++17
- Java 11
- Pascal
- Perl
- Python 2 / Python 3

Support plagiarism detection via [Stanford MOSS](https://theory.stanford.edu/~aiken/moss/).

## Installation

Most of the setup are the same as DMOJ installations. You can view the installation guide of DMOJ here: https://docs.dmoj.ca/#/site/installation.
There is one minor change: Instead of `git clone https://github.com/DMOJ/site.git`, you clone this repo `git clone https://github.com/LQDJudge/online-judge.git`.

### Additional Steps in Production:

1. To use newsletter (email sending), go to admin and create a newsletter.
2. Change the domain name and website name in Admin page: Navigation Bars/Sites

### Some frequent difficulties when installation:

1. Missing the `local_settings.py`. You need to copy the `local_settings.py` in order to pass the check.
2. Missing the problem folder in `local_settings.py`. You need to create a folder to contain all problem packages and configure in `local_settings.py`.
3. Missing static folder in `local_settings.py`. Similar to problem folder, make sure to configure `STATIC_FILES` inside `local_settings.py`. 
4. Missing configure file for judges. Each judge must have a seperate configure file. To create this file, you can run `python dmojauto-conf`. Checkout all sample files here https://github.com/DMOJ/docs/blob/master/sample_files.

## Usage

Suppose you finished all the installation. Everytime you want to run a local server, follow these steps:

1. Activate virtualenv:
```bash
source dmojsite/bin/activate
```

2. Run server:
```bash
python manage.py runserver 0.0.0.0:8000
```

3. Create a bridge (this is opened in a different terminal with the second step if you are using the same machine)
```bash
python manage.py runbridged
```

4. Create a judge (another terminal)
```bash
dmoj 0.0.0.0 -p 9999 -c <path to yml configure file>
```
Here we suppose you use the default port 9999 for bridge in `settings.py`. You can create multiple judges, each should be in a seperate terminal.

**Optional**

5. Run celery worker (This is server's queue. It may be necessary in some functions)
```bash
celery -A dmoj_celery worker
```

6. Run a live event server (So everything is updated lively like in the production)
```bash
node websocket/daemon.js
```

## Deploy
Most of the steps are similar to Django tutorials. Here are two usual steps:

1. Update vietnamese translation:
 - If you add any new phrases in the code, ```python manage.py makemessages```
 - go to `locale/vi`
 - modify `.po` file
 - ```python manage.py compilemessages```
 - ```python manage.py compilejsi18n```

2. Update styles (using SASS)
 - Change .css/.scss files in `resources` folder
 - ```./make_style && python manage.py collectstatic```
 - Sometimes you need to `Ctrl + F5` to see the new user interface in browser.
 
## Screenshots

### Leaderboard

Leaderboard with information about contest rating, performance points and real name of all users.

![](https://i.imgur.com/ampxHXM.png)

### Admin dashboard

Admin dashboard helps you easily managing problems, users, contests and blog posts.

![](https://i.imgur.com/iccr3mh.png)

### Statement editor

You can write the problems' statement in Markdown with LaTeX figures and formulas supported.

![](https://i.imgur.com/CQVC754.png)

### Chat

Users can communicate with each other and can see who's online.

![](https://i.imgur.com/y9SGCgl.png)
