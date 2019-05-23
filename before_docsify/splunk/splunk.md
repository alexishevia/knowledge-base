# Splunk

## Resources

### Docs
- [Getting Started](https://www.splunk.com/en_us/resources/getting-started.html)
- [Dashboards and Visualizations](http://docs.splunk.com/Documentation/Splunk/7.0.3/Viz/Aboutthismanual)
- [Search Reference](http://docs.splunk.com/Documentation/Splunk/7.0.3/SearchReference/Whatsinthismanual)
- [stats, eventstats, and streamstats](https://www.splunk.com/blog/2014/04/01/search-command-stats-eventstats-and-streamstats-2.html)
- [Reusing queries in a dashboard](http://docs.splunk.com/Documentation/Splunk/6.6.2/Viz/Savedsearches#Post-process_searches)

### Videos
- [Dashboarding Fun In Splunk Enterprise 6](https://www.youtube.com/watch?v=d4GW6KmBgHQ)
- [Splunk Tutorials : Adding Dropdown Filters to Dashboards](https://www.youtube.com/watch?v=1Z06q9gMlac)
- [Network Monitor in 10 minutes with Splunk](https://www.youtube.com/watch?v=HPVlHQjnxYs)

### Courses
- [Splunk Fundamentals](https://www.splunk.com/en_us/training/free-courses/splunk-fundamentals-1.html)

### Projects & Repos
- https://github.com/foxbroadcasting/splunk_dashboards

## Concepts
Splunk is made of 3 components:
- Forwarders: send data into Splunk
- Indexers: process incoming data, normalize and store it
- Search Heads: parse search requests, send data processing requests to indexers, aggregate results into dashboards, reports, etc

Splunk supports 3 data sources:
- Static Files: upload a static file
- Monitor: monitors logs and other file systems from the same machine where Splunk is installed
- Forwarders: grab data from outside sources

## Local Installation
I installed Splunk in my machine using the provided `.deb` file.
Splunk files are located in the `/opt/splunk` directory, and are owned by the `splunk` user.

I created a couple users:
- Admin user: admin/infinitystones
- Power user: uname/5p1unkbcup

Run Splunk: 
```
cd /opt/splunk/bin
sudo su splunk
./splunk start
./splunk stop
./splunk help
```

## Search Commands
- `fields`: specify which fields to be returned (can improve performance)
    eg: `| fields foo, bar`
- `table`: render specific fields as a table. Like `fields`, it can also improve performance
    eg: `| table foo, bar`
- `rename`: rename a field
    eg: `| rename oldFieldName AS "New Field Name"`
- `dedup`: remove duplicate values
    eg: `| dedup userip`
        `| dedup firstname lastname`
- `sort`: sort results
    eg: `| sort -salePrice +productName limit=20`
- `top`: find the most common values of a given field
    eg: `| top Vendor limit=20`
- `rare`: show the least common values of a given field
    eg: `| rare Vendor limit=20`
- `stats`: produce statistics. uses sub-commands:
    * `count`: returns number of events
    * `distinct_count`: count of unique values
    * `sum`: sum of numeric values
    * `avg`: average of numeric values
    * `list`: list of all values of a given field
    * `values`: list unique values of a given field

## Lookups
After uploading a lookup table file, we can inspect its values by running:
`| inputlookup <filename>` eg: `| inputlookup uplynk_channels_lookup.csv`

We can also use the lookup in our searches:
`<search> | lookup <filename> <input_field> OUTPUT <output_field>`
eg:
`sourcetype=aws:s3 | lookup uplynk_channels_lookup.csv channel_id OUTPUT channel_name`

Note: use `OUTPUTNEW` instead of `OUTPUT` to keep from overwriting existing fields with your Lookup.

If we define a lookup definition, the syntax can be modified to:
`<search> | lookup <lookup_definition_name> <input_field> AS <output_field>`
