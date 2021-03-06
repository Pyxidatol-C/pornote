# pornote

This project is a parody of the famous french homework online system [Pronote](https://fr.wikipedia.org/wiki/Pronote). Pornote enables you to share your homework instead of receiving it, and rewards you with other homework from people of your own class !

Pornote was an original idea of [Gnomino](https://github.com/Gnomino), that I found funny and wanted to actually make so I could in the meantime progress in Python, a new language I just started to learn about.

## How does it work ?

Each person of a class creates an account, and everyone can upload homework to the server (but not everyone can access your homework, only those who worked for !). When you upload it, you gain a point, but you can also decide to upload it publicly so that it's free for everyone, and for three homework published publicly, you gain an extra point for generosity. These points are needed to access other people's homework, so that everyone has to work a bit to get rewarded.

## What does it look like ?

![Homepage](/img/homepage.png)

## What is pornote using ?

Pornote is using [Flask](http://flask.pocoo.org/), a microframework for [Python](https://www.python.org/), and some other libraries like [flask-sqlalchemy](http://flask-sqlalchemy.pocoo.org/2.1/) (for the database), and [werkzeug](http://werkzeug.pocoo.org/) (to handle password storage).

## Run pornote on your server

*Don't forget that I created this especially for my school/class, so it may not be fully compatible with your system (if you want to use it also).*

First, you must create the database :

```bash
$ python manage.py db init
$ python manage.py db migrate
$ python manage.py db upgrade
```

Then, you need to create a `config.py` file, there is a template called `default_config.py` in the `pornote` directory that you can copy. Don't forget to change the secret key in the configuation file before using it ! Also, you should set the location of your `upload` folder, by changing the `UPLOAD_FOLDER` value in the config file. And finally, you might consider changing the `UNALLOWED_EXTENSIONS` value to prevent from XSS problems on your server.

I personnaly use [nginx](https://www.nginx.com/) on my Raspberry Pi to run the server, and I have [CloudFlare](https://www.cloudflare.com/) handling DNS for me. I chose [gunicorn](http://gunicorn.org/) to deploy pornote, and I have [supervisor](http://manpages.ubuntu.com/manpages/intrepid/man3/supervisor.3erl.html) installed to easily manipulate the server. You can find the nginx config in the `pornote.conf` file and the supervisor config in `pornote_supervisor.conf`.
