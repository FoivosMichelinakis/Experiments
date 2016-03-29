
# Experiment
Evaluate http download speed.

The experiment will with a configurable interval download a .zip file over http using curl.

The required parameters to run the container are 
 * interface -- The local interface to bind to
 * max_size -- The maximum size in Kbytes to download (for now this is capped at 1000MB)
 * max_time -- The maximum time in seconds a single download are allowed to take
 * interval -- How long time between execution of the downloads, IF the actual download time => interval. The next file download fill start when latter is finished.

The download will abort when either Max size OR Max time OR 1001MB is downloaded.    
More information, e.g. url and options used can be found in files/run.sh and files/curl_wrapper.py


## Requirements

These directories must exist and be writable by the user/process running curl_formatter.py:   
/output/    
/tmp/    


## Example usage
```bash
curl -o /dev/null --raw --silent --write-out "{ remote: %{remote_ip}:%{remote_port}, size: %{size_download}, speed: %{speed_download}, time: %{time_total}, time_download: %{time_starttransfer} }" --interface eth0 --max-time 100 --range 0-100 http://speedtest.bahnhof.net/1000M.zip| python curl_formatter.py
```

## Docker misc usage

docker ps  # list running images
docker exec -it [container id] bash   # attach to running container
