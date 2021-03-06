# crawler-hbase
a library to interact with the crawler tables stored in hbase.
crawler hbase exports two modules: class called Client which constructs an hbase client and a module Utils which is an object containing helper functions.

## Class Client
```javascript
var HbaseClient = require("crawler-hbase").Client;
var client = new HbaseClient("0.0.0.0:9090");
```

#### CrawlHbaseClient(dbUrl)
Constructs the client using the provided hbase dbUrl. It is assumed that there is Hbase-thrift running on the provided dbUrl.


#### storeRawCrawl(crawl)
Stores a raw crawl into table raw_crawls.

#### getRows(startKey, endKey, limit, descending, tableName, filterString)
The generic get function used by almost all the other specific gets

#### getLatestRawCrawl()
Returns the latest raw crawl.

#### getRawCrawlByKey(key)
Gets a raw crawl by key.

#### storeProcessedCrawl(newCrawl, oldCrawl)
Stores newCrawl. oldCrawl is used to calculate the changes that happened between the two crawls.

#### getCrawlInfo(crawlKey)
Get crawl info.

#### getNodeHistory(pubKey)
Get the array of all different versions tha given node appeared in crawls.

#### getCrawlNodeStats(crawlKey)
Get stats about the given nodes in the given crawl

#### getConnections(crawlKey, pubKey, type)
Get links between nodes. type is either 'in' or 'out' to get ingoing or outgoing connections respectively.

#### getAllConnections(crawlKey)
Get all links for the given crawl

## Utils
provides helper methods to work with hbase tables' keys which have a lot of hidden information in them.

#### keyToStart(key)
Get crawl start time from crawl's key

#### keyToEnd(key)
Get crawl end time from crawl's key