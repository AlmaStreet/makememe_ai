# [makememe.ai](http://makememe.ai/)

This project allows users can create memes in under 5 seconds by describing them with natural language. The AI system transforms the user's input into a meme. This project is a fun way for software developers to learn about AI and Python development.

You are welcome to fork this repo and make adjustments or contributions. If you fork or clone the repo, it is first required to review OpenAI's [go live policy](https://beta.openai.com/docs/going-live). You will need your own access and key in order to contribute.

## [The Site](http://makememe.ai/)

<img src="media/makememe-homepage.png" width="600" alt="makememe.ai home page"></img>

## [The Demo](https://www.producthunt.com/posts/makememe-ai)

[![makememe.ai demo video](https://img.youtube.com/vi/wZ6KCDAcKws/0.jpg)](https://www.producthunt.com/posts/makememe-ai)

# Setup the website locally

There are three steps required to get the makememe.ai app to run on your computer. If you are not familiar with the technology stack I highly recommend [Corey Schafer's](https://www.youtube.com/channel/UCCezIgC97PvUuR4_gbFUs5g) Youtube series on [Python Flask Tutorial: Full-Featured Web App](https://www.youtube.com/watch?v=MwZwr5Tvyxo). The series goes over Flask and Postgres in detail. To learn more about the AI, I recommend reading my Medium post How To Make Memes with AI in Python (coming soon).

1. Run Flas server
2. Install OpenAI Key
3. Install and run Postgres server

## 1. Run Flask Server

See the [code series](https://joshbickett.medium.com/making-memes-with-ai-db3332fc00ac) to learn more about the code base and how to contribute to the project.

Create a [virtual environment](https://docs.python.org/3/library/venv.html)

```
python3 -m venv venv
```

Activate the environment

```
source venv/bin/activate
```

Install all packages into venv

```
pip3 install -r requirements.txt
```

Run

```
python run.py
```

## 2. Install and run Postgres server

If you do not have Postgres installed, you will need to install it on you computer.

Homebrew is also required to install Postgres. Homebrew's [webpage](https://brew.sh/) has a tutorial.

Mac users you can install Postgres with the following [Homebrew command](https://formulae.brew.sh/formula/postgresql):

```
brew install postgresql
```

When Postgres is installed with Homebrew a postgres user needs to be created with the command below.

```
 /usr/local/opt/postgres/bin/createuser -s postgres
```

The next step is to start the Postgres service

```
brew services start postgresql
```

Now we can create the database for the application with the command below

```
createdb makememe
```

The next few commands need to be executed in the project directory. If you are not in that directory, please navigate there now with the (cd - change directory command).

Once you are in the project directory, make sure the virtual environment is activated (should show (venv) next to terminal user). If not activate it with the command - source venv/bin/activate

Now open the python terminal by typing the command below

```
python
```

Finally, we will create the database tables in the python terminal with the commands below

```
from makememe import db
db.create_all()
db.session.commit()
```

Now you can exit.

```
exit()
```

## 3. Create Config file that includes an OpenAI Key

In order to run the project locally a few pieces of information need to be setup in a config file. Follow the steps below to setup prepare the project.

The first step is to create the following file (with a matching directory path).

```
/etc/make_meme/config.json
```

Once the file is created, populate it with some information.

Flask requires a secret key to sign cookies. You can learn more about it [here](https://explore-flask.readthedocs.io/en/latest/configuration.html).

OpenAI provides a key when receive access to the API. The local project uses your key when making OpenAI API request. The request and billing will show up under your account. Assuming you are running the project for testing and development reasons, the cost should be small.

The project also requires a file with font information. It uses that font to display the text on the image.

Lastly, a database URI for Postgres is required. This information should be available from the setup in step 2.

```
{
        "SECRET_KEY": "~a Flask secret key here~",
        "OPEN_AI_KEY": "~your key~",
        "FONT_PATH": "~path to a font~",
        "DB_URI": "~your Postgres URI~"
}
```

Once this file is created then the project should be ready to run..

Navigate to the project directory and make sure the virtual environment is running (venv). Type the command below.

```
python run.py
```

Now you can enter the local server URL (below) in your web browser and you should see the app.

```
http://127.0.0.1:5000/
```
