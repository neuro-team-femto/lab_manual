# Running an online study


## Installing and running a JONES study locally (without the internet)

- install the GO programming language on your machine [https://go.dev/doc/install](https://go.dev/doc/install)

- cd to the directory where you want the experiments to be stored (e.g. `C:/work/projects/`) & clone the jones repository there
```
cd C:/work/projects/
git clone https://github.com/neuro-team-femto/jones.git .
```
This should create a `/jones/` directory

- copy your experiment to the `jones/data` folder (e.g. `jones/data/my_exp`). If you just want to try the procedure, you can copy one experiment from the `jones/examples` folder (e.g. `image_int1`) 

- cd to the `jones` directory and build the jones resources: you do this by asking `go` to run the program stored in `jones/main.go` with the `-APP_MODE BUILD_FRONT` tag. This builds the javascript ressources that the application needs to run properly 
```
cd jones
go run main.go -APP_MODE BUILD_FRONT
```

- then run the application, by calling `go run` again, this time without the `-APP_MODE` tag
```
go run main.go
```
This starts the application, which starts serving html pages that are available locally via localhost (i.e. you don't need an internet connection, but it can of course only be accessed on your machine). By default, the application listens to interactions occurring on port 8100 (which is why you'll need to connect to `localhost:8100` below).  

- to run the experiment, open a browser and go to [http://localhost:8100/xp/my_exp/new](http://localhost:8100/xp/my_exp/new). You should be able to create a user and start responding to the experiment. All results will be stored in `jones/data/my_exp/results`.

## Deploying JONES updates on server

These instructions are for upgrading JONES on the already installed server neuro-xp.femto-st.fr

### Connect to server

- open a shell / command prompt (note: SublimeText REPL stdin is not a terminal and won't work; use command prompt on windows)
- ssh to the server: (172.20.208.18 or neuro-xp.femto-st.fr)
```
> ssh admin@172.20.208.18
```
- admin password is `aqzsedrftg`

### Upload new code and build

- cd to /opt/revcor_test/ (note: you may have to cd .. to exit the `admin` home)
- clone the version of jones you want to install (`.` at the end tells to clone directly into `revcor_test` and not `revcor_test/jones/`)
```
git clone https://github.com/neuro-team-femto/jones.git .
```
- build jones on server:
```
go build
./jones -APP_MODE BUILD_FRONT
```

### Test new code
- test it by running the ./jones app: first copy an experiment from /example to /data, then run the app using the APP_ORIGINS keyword so that it listens to https://neuro-xp.femto-st.fr
```
APP_ORIGINS=https://neuro-xp.femto-st.fr ./jones
```
!!! warning
  
  Not sure what happens if you have the prod app already running in a screen and listening to the same https: you may need to kill it first before you can APP_ORIGINS to the test app. This will interrupt service. 
  
- test that the app works, by navigating to `https://neuro-xp.femto-st.fr/xp/image_int1/new` (or whatever your experiment name is)
- CTRL+C to break the app

### Deploy to prod
If this works, then deploy by replacing revcor_prod by revcor_test: 

- copy the content of the prod/data folder (all experiments) into test
```
cp -r /opt/revcor_prod/data/* /opt/revcor_test/data
```
- delete the old backup
```
rm -r /opt/revcor_prod.backup
```
- backup the current prod
```
mv /opt/revcor_prod /opt/revcor_prod.backup
```
- rename test as prod
```
mv /opt/revcor_test/revcor /opt/revcor_prod
```

### Run app in a persistent terminal (GNU Screen)

If revcor_prod/jones isn't already running in a persistent terminal, we need to run it
```
screen -R
cd /opt/revcor_prod
APP_ORIGINS=https://neuro-xp.femto-st.fr ./jones
```

- test on https://neuro-xp.femto-st.fr/xp/image_int1/new

- if works, detach the GNU Screen so that another user/session can access the process
```
CTRL+A,D
```

## Running, Stopping the app

### Exec
- ssh to serveur
```
> ssh admin@172.20.208.18
```
- admin password is `aqzsedrftg`
- launch a new persistent terminal (GNU Screen)
```
screen -R
```
- run the app
```
cd /opt/revcor_prod
APP_ORIGINS=https://neuro-xp.femto-st.fr ./jones
```
detach the GNU Screen so that another user/session can access the process
```
CTRL+A,D
```

### Stopping the app

- ssh to serveur
```
> ssh admin@172.20.208.18
```
- admin password is `aqzsedrftg`
- launch a new persistent terminal (GNU Screen)
```
screen -R
```
- kill the process
```
CTRL + C
```

## Adding a new experiment

This is for adding new experiments in an already-running app

The easiest is probably to install a GUI file transfer app like WINSCP. 
- Connect to the server
```
server: 172.20.208.18
port: 22
user: admin
pass: aqzsedrftg
```
- copy your experiment folder into `opt/revcor_prod/data` (-> `opt/revcor_prod/data/my_exp`) 
- test on https://neuro-xp.femto-st.fr/xp/my_exp/new

## User instructions

### 1. Logging In:
- Visit the experiment link: (https://neuro-xp.femto-st.fr/revcor/xp/prosavc/new).
- Enter the login credentials: Username (identifiant): ex:frank, Access Code (Code d'accès): prosavc0aa0mv0jj.
- Click "valider" to log in.

## Initial Setup
### 2.User Information:
- Enter your age as "99" (*).
- For gender, select "-" (*).
- Click "valider" to proceed.
  
*indicating a confidential state in which we don't want to save the personal information of the participant

## Understanding the Experiment
### 3.Procedure Overview:
- You will hear different pronunciations of the word "vraiment?" (English: "Really?").
- Your task is to identify which pronunciation sounds more like a question.
- Press space to begin the experiment.

## Conducting the Experiment
### 4. Listening to Pronunciations:
- Press space to hear the first pair of sounds.
- Decide which pronunciation sounds more like a question.
- If the first sound is your choice, press "f". If it's the second sound, press "j".
- After making a selection, the next pair of sounds will play automatically.
- Repeat this process for each pair of sounds until the end of the experiment.

## Accessing the results 

*For Experimenters and the ProsAVC Team in APHP

### 1. Administrator Access:

- To view individual or collective participant results, go to : https://neuro-xp.femto-st.fr/revcor/xp/prosavc/results
- Use Username (Identifiant): "admin" and Password: "prosavc_admin".
- Click "sign-in" to access the experiment's dashboard.

### 2. Reviewing Participant Data:

- Upon successful login, you'll be presented with a list of CSV files, each corresponding to a participant's data.
- Click on a CSV file to review the participant's results.
- You have the option to download the file for further analysis.

