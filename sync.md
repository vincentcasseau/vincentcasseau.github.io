---
layout: page
title: Synchronisation
--- 

### OF-v1706   
{: #OF-v1706 }

1. Change the current working directory to your local *hyStrath* repository
```sh 
cd $WM_PROJECT_USER_DIR/hyStrath
```
2. Grab online updates and merge them with your local work
```sh
git pull origin master  
``` 
3. Decide which module(s) you wish to synchronise:
```sh
./install.sh 8 2>/dev/null
```

where _8_ is the number of processors to be used during the synchronisation (it can be edited).
