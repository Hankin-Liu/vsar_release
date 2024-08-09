# vsar_release
Publish vsar release package. 

## Purpose
Provide a design plan to make sar's output visualized.
Currently, this software reads sar's output through a pipe, and writes output data into influxdb for visualization.

## Version
Run sh start.sh -v

## Copyright
Copyright (c) 2024 Liu Hua Jun
All rights reserved.     
Do not use it for commercial purposes.     

## Usage
Run sh start.sh -h
### realtime mode
Run "sh start.sh -u [influxdb write url] -H [host ip or name]", it will write sar's output into influxdb in realtime.
### offline mode
First, you must have a command to generate sar's output. Then use -s to specify this command.
For example:
1. You can run "sar -A 1 -l ./sar.log" for a while and generate offline file sar.log.
2. Run "sh start.sh -u [influxdb write url] -H [host ip or name] -s 'sar -A 1 -f ./sar.log'", it will write sar's output of the offline file into influxdb.

## Deployment   
1. Enter deploy folder.   
2. Add your machines' ip, user, password, deploy_path, influxdb_url, batch_count into hosts file.  
3. sh deploy.sh   

## Operation and maintenance   
### Start vsar on all machines   
1. Enter deploy folder.   
2. sh start.sh   
### Stop vsar on all machines   
1. Enter deploy folder.   
2. sh stop.sh   
