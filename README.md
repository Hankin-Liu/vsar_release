# vsar_release
Publish vsar release package. 
    
## Purpose
Provide a design plan to make [sar,pidstat]'s output visualized.
Currently, this software reads [sar,pidstat]'s output through a pipe, and writes output data into influxdb for visualization. 

## Version
Run sh start.sh -v

## Copyright
Copyright (c) 2024 Liu Hua Jun
All rights reserved.
Do not use it for commercial purposes.

## Usage
Run sh start.sh -h
### realtime mode
Run "sh start.sh -u [influxdb write url] -H [host ip or name]", it will write sar's data into influxdb in realtime.
### offline mode
First, you must have a command to generate sar's output. Then use -s to specify this command.
For example:
1. sar
   (1) You can run "sar -A 1 -l ./sar.log" for a while and generate offline file sar.log.
   (2) Run this program in order to write sar's output of the offline file into influxdb.
       For influxdb v1 api: sh start.sh -u "http://localhost:8086/write?db=db_name" -H "127.0.0.1" -s "sar -A 1 -f ./sar.log" -b 20
       For influxdb v2 api: sh start.sh -u "http://localhost:8086/api/v2/write?bucket=db_name\&org=HOME\&precision=ns" -t "pR7LoUgVRNPt11t2fQqkYGc8GA8dw0rHbiwLJB35wdkqNZuXDxO2WsNvFKlGie9czu4Bnr-54P-zJcP7jTs7Dw==" -H "127.0.0.1" -s "sar -A 1 -f ./sar.log" -b 20
2. pidstat
   (1) You can run "pidstat -u -d -r 1 -U user_name > pidstat.log" for a while and generate offline file pidstat.log.
   (2) Run this program in order to write pidstat's output of the offline file into influxdb.
       For influxdb v1 api: sh start.sh -u "http://localhost:8086/write?db=db_name" -H "127.0.0.1" -s "cat ./pidstat.log" -b 20
       For influxdb v2 api: sh start.sh -u "http://localhost:8086/api/v2/write?bucket=db_name\&org=HOME\&precision=ns" -t "pR7LoUgVRNPt11t2fQqkYGc8GA8dw0rHbiwLJB35wdkqNZuXDxO2WsNvFKlGie9czu4Bnr-54P-zJcP7jTs7Dw==" -H "127.0.0.1" -s "cat ./pidstat.log" -b 20

## Deployment
1. Enter deploy folder.
2. Add your machines' ip, user, password, deploy_path, influxdb_url, influxdb_token, batch_count into hosts file.
3. sh deploy.sh

## Operation and maintenance
### Start vsar on all machines
1. Enter deploy folder.
2. sh start_all.sh
Note: start_all.sh will run both 'sar -A 1' and 'pidstat -d -u -r 1 -U user_name' on destination server.
### Stop vsar on all machines
1. Enter deploy folder.
2. sh stop_all.sh     
