---
layout: post
title: Getting Chrome Debugger to work in VS Code with Windows Subsystem for Linux
date: '2019-03-24 21:20:03'
---

I had created a React app (using create-react-app) under my Windows Subsystem for Linux (WSL) environment on Windows 10 and wanted to debug from Visual Studio Code using the Chrome Debugger.

The first and commonly known step to open WSL folders in VS Code is to make sure the source directory is somewhere on your actual windows filesystem such as `/mnt/c/Users/dan/development/web-app` etc.

> As a side note, I created a symlink to my development folder under my WSL home to avoid having to `cd` in here all the time e.g. `ln -s /mnt/c/Users/dan/development ~/development`

Even with this, and with VS Code happilly finding the files and launching and attaching to Chrome, breakpoints were never hit and were disabled with the `breakpoint unverified` message. 

VS Code specifically talks about some support they added for debugging node apps under WSL with the addition of a `"useWsl" : true` setting that can be added to the `launch.json` file, but this is a complete red herring.

The magic sauce is to add `/mnt/c/*": "C:\\*` to the `sourceMapPathOverrides` section as [detailed by elliotbe in his gist on github](https://gist.github.com/elliotbe/7d0106f98fd0b61215e0ae423ee01b180)

My full `launch.json` now looks as follows:

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome against localhost",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceFolder}",
            "trace": true,
            "sourceMapPathOverrides": {
                "/mnt/c/*": "C:\\*"
            }
        }
    ]
}
```

Hope this helps!
