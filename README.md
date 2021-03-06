# ekg-elasticsearch: elasticsearch backend for ekg

This library lets you send metrics gathered by the ekg family of packages (e.g.
[ekg-core](https://hackage.haskell.org/package/ekg-core) and
[ekg](https://hackage.haskell.org/package/ekg)) to
[elasticsearch](https://www.elastic.co/products/elasticsearch). The metrics sent
are in the same format as [beats](https://www.elastic.co/products/beats) metrics.

# Getting started

Exporting metrics to elasticsearch is simple. Either create an empty metric
store and register some metrics

```haskell
import System.Metrics
import System.Remote.Monitoring.ElasticSearch

main = do
    store <- newStore
    registerGcMetrics store
    forkElasticSearch defaultESOptions store
    ...
```

or use the default metrics and metric store provided by the ekg
package

```haskell
import System.Remote.Monitoring
import System.Remote.Monitoring.ElasticSearch

main = do
    handle <- forkServer "localhost" 8000
    forkElasticSearch defaultESOptions (serverMetricStore handle)
    ...
```

`forkElasticSearch` starts a new thread the will periodically send your
metrics to elasticsearch using a bulk request.

# Get involved!

Please report bugs via the
[GitHub issue tracker](https://github.com/cdodev/ekg-elasticsearch/issues).

Master [git repository](https://github.com/cdodev/ekg-elasticsearch):

    git clone https://github.com/cdodev/ekg-elasticsearch.git

# Authors

This library is written and maintained by Ben Ford,
<ben@perurbis.com>.
