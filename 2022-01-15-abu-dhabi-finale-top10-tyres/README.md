
Pit stop data obtained through the [ergast API](https://ergast.com/mrd/).
```
curl -s http:///ergast.com/api/f1/2021/22/pitstops.json > abu-dhabi-pitstops.jsomn
```

```shell
#!/bin/zsh

drivers=(max_verstappen hamilton sainz tsunoda gasly bottas norris alonso ocon leclerc)

for driver in $drivers; do
    # Race start
    echo "17:00:00" >> $driver.csv

    # Pit stops
    print "$(cat abu-dhabi-pitstops.json | jq -r ".MRData.RaceTable.Races[0].PitStops | map(select(.driverId==\"$driver\")) | map([.time] | join(\",\")) | join(\"\n\")")" >> $driver.csv

    # Race end (leader finish)
    echo "18:30:18" >> $driver.csv
Done
```
