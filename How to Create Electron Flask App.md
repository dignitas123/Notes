cd ~
mkdir yourproject
mkdir App

// create flask and electron folder

// install electron quick build into electron folder
// https://www.youtube.com/watch?v=OVY4ifYy3UI clone from this video the python files https://github.com/shahriar0247/python-electron

cd ~/yourproject/App/flask

## create environment

python3 -m venv yourEnvironment

## activate environment

. yourEnvironment/bin/activate

## install if new pacakges used

pip install -e .

## only now: time to create the folder with an executable. ":" in linux, ";" in windows

pyinstaller --add-data="templates:templates" --add-data="static:static" \flask_server.py

## now copy the whole folder in an electron folder

### in main.js

### after 'createWindow() {'

```
let exectuablePath = 'flask_server/flask_server'; // linux and windows different?
  let child = require('child_process').exec;

  child(exectuablePath, function (err, data) {
    if (err) {
      console.error(err);
      return;
    }
    console.log(data.toString());
  })
```

## NOTE

Make sure you delete build, dist folder and spec file before making a new

### after 'const mainWindow' declaration

```
  const urlExist = require("url-exist");

  (async () => {
    const exists = await urlExist("http://127.0.0.1:5000/");
    // Handle result
    mainWindow.loadURL("http://127.0.0.1:5000/")
  })();
```

### after 'mainWindow.loadFile('index.html')'

```
  mainWindow.on('closed', function(){ 
    // kill the server on exit 
    const { exec } = require('child_process');
    let taskkillCom = 'taskkill /f /t /im flask_server.exe'

    if (window.navigator.userAgent.indexOf("Mac") != -1 || window.navigator.userAgent.indexOf("X11") != -1
        || window.navigator.userAgent.indexOf("Linux") != -1)
        taskkillCom = 'killall -KILL flask_server'
    exec(taskkillCom, (err, stdout, stderr) => { 
      if (err) { 
        console.log(err) 
        return; 
      } 
      // the *entire* stdout and stderr (buffered) 

      console.log(`stdout: ${stdout}`); 
      console.log(`stderr: ${stderr}`); 
    }); 
  });
```

## do this before 'npm start'

cd ~/yourproject/App/electron

npm install url-exist

