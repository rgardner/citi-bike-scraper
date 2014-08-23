# Citi Bike Trips Downloader
Download your Citi Bike trip data from [the Citi Bike
website](https://citibikenyc.com/member/trips) into usable CSV files.

## Getting Started
### Quick Setup
```
wget https://github.com/rgardner/citi-bike-scraper/blob/master/download_trips.rb
gem install mechanize
gem install trollop
```

### Usage
```
$ ./download_trips.rb -h
Download Citi Bike trip data
       --dry-run, -d:   Log trips to stdout, do not save to file.
  --username, -u <s>:   Your Citi Bike username
  --password, -p <s>:   Your Citi Bike password
         --n, -n <i>:   Number of months to download
          --help, -h:   Show this message
```

## CSV Format
After running `ruby download_trips.rb`, there will be a data directory
containing all of the CSV files. They are named `month-YYYY.csv`. Each file
contains that months' trips stored in the following format:
```
unique_trip_id, start_station, start_time, end_station, end_time, trip_duration
int, string, datestring, string, datestring, durationstring
```
where `datestring` is `%m/%d/%y %l:%M:%S %p` and duration string is `%dm %ds`.


## No Data Processing
CB-Scraper leaves the all data processing to you. This script **does not**
change your data in any way. Empty fields will be saved as empty strings.

If you encounter trip data like this:
```
unique_trip_id,start_station,start_time,Trip Completed, Trip Completed,,
```
your trip did not end normally. In my experience, this occurs when I docked the
bike incorrectly and called to manually end my trip.
