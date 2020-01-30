# RASAS-VOF
Rasa step-wise documentation

### Installation guide:
1. Install the Python development environment:

Check if your Python environment is already configured:
$ python3 --version
$ pip3 --version
If these packages are already installed, these commands should display version numbers for each step, and you can skip to the next step.
 
Otherwise, proceed with the instructions below to install them.
 
Ubuntu:
Fetch the relevant packages using apt, and install virtualenv using pip.
$ sudo apt update
$ sudo apt install python3-dev python3-pip
 
macOS:
Install the Homebrew package manager if you haven’t already.
Once you’re done, you can install Python3.
$ brew update
$ brew install python
 
Windows:
Make sure the Microsoft VC++ Compiler is installed, so python can compile any dependencies. You can get the compiler from Visual Studio. Download the installer and select VC++ Build tools in the list.
Install Python 3 (64-bit version) for Windows.
C:\> pip3 install -U pip
 
2. Create a virtual environment (strongly recommended)
Ubuntu/macOS:
Create a new virtual environment by choosing a Python interpreter and making a ./venv directory to hold it:
$ python3 -m venv --system-site-packages ./venv
 
Activate the virtual environment:
$ source ./venv/bin/activate
 
 
 
 
Windows:
Create a new virtual environment by choosing a Python interpreter and making a .\venv directory to hold it:
C:\> python3 -m venv --system-site-packages ./venv
Activate the virtual environment:
C:\> .\venv\Scripts\activate
 
You can also create an environment using anaconda navigator. For more information, refer to the documentation in the link.
https://docs.anaconda.com/anaconda/navigator/getting-started/ 
 
3. Install Rasa Open Source
Ubuntu / macOS / Windows:
First make sure your pip version is up to date:
$ pip install -U pip
 
To install Rasa Open Source:
$ pip install rasa
 
Setting up files:
1) Make a new folder for the bot and save all the bot related files in it. Let’s name the folder “rasa” for convenience.
 
2) Under “rasa” folder, make a folder named “data” and add the two files namely “stories.md” and “nlu.md”.
“Stories.md” file contains the story data and “nlu.md” contains the intents. 
 
3) Under “rasa” folder, make another empty folder named “models”. This is where our trained models will be saved.
 
4) Under “rasa” folder, make a “config.yml” file where the pipelines and policies used will be mentioned. It is configuration of your NLU and Core models.
 
5) Under “rasa” folder, make a “domain.yml” file where all the intents and actions along with the templates will be mentioned.
 
6) Under “rasa” folder, make a “credentials.yml” file where the details for connecting to other services is mentioned.
 
7) Under “rasa” folder, make a “endpoints.yml” file where the details for connecting to channels like fb messenger is mentioned.
 
8) Under “rasa” folder, make a “__init__.py” file. Its an empty file that helps python find your actions.
 
9) Under “rasa” folder, make a “actions.py” file where code for your custom actions is mentioned.
 
### Training and running the bot:
 
In command prompt, activate your environment and go to the “rasa” folder location. Then run the following commands.
 
1) To train:
     rasa train
 
2) To run the bot:
     rasa shell
 
Now your bot is running and you can give input messages.
 
Integrating the bot to personal website:
 
1) add the below configuration in the credentials.yml file:
 
socketio:
  user_message_evt: user_uttered
  bot_message_evt: bot_uttered
  session_persistence: true
 
2) start your bot using the below command. Type this command in another cmd terminal.
rasa run -m models --enable-api --cors "*" --debug
 
 
 
 
 
 
 
 
 
3) After running the above command, check where the rasa server is starting on. Here it's on “5005”.
 

 
4) Now go to this link https://github.com/botfront/rasa-webchat and add the code in “body” tag of your html page or copy the below code under “body” tag.
<div id="webchat"/>
<script src="https://storage.googleapis.com/mrbot-cdn/webchat-latest.js"></script>
// Or you can replace latest with a specific version
<script>
  WebChat.default.init({
    selector: "#webchat",
    customData: {"language": "en"}, // arbitrary custom data. Stay minimal as this will be added to the socket
    socketUrl: "http://localhost:5005", //take note, the 5005 is because our rasa server is working on 5005 
    socketPath: "/socket.io/",
    title: "Title",
    subtitle: "Subtitle",
  })
</script>
 
Note: In the above code, change the socket url port number to our rasa server's port number. Also make sure in the “credentials.yml” file this is added:
rasa:
  url: "http://localhost:5005/api" 
(5005 because rasa server port number is 5005)
 
4) Now open the webpage and the bot widget should be present and working.
 

__________________

 ### For adding an image:
 
 Below is the format of adding a image into the bot. We cannot directly add the image
 Instead we add the Url of the image in the *domain.yml* in the templates as:
 
 
    utter_cheer_up:

       - text: "Here is something to cheer you up:"

         image: "https://i.imgur.com/nGF1K8f.jpg"

  __________

 ### For adding a link
 
 For adding link in the bot, add the following code in the *template* of domain.yml
 
 
    utter_link:

       - text: "Please click link to continue: [click here for link](https://www.google.com/)"
 
 
 
 
 



