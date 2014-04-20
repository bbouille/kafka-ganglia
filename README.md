# Kafka Ganglia Metrics Reporter

This is a simple reporter for kafka using the [GangliaReporter][]. It
works with kafka 0.8 beta and 0.8.1 version.

## Install On Broker

1.  Build the `kafka-ganglia-1.0.0.jar` jar using `mvn package`.
2.  Add `kafka-ganglia-1.0.0.jar` and `metrics-ganglia-2.2.0.jar` to the
    `libs/` directory of your kafka broker installation
3.  Configure the broker (see the configuration section below)
4.  Restart the broker

## Configuration

Edit the `server.properties` file of your installation, activate the
reporter by setting:

    kafka.metrics.reporters=com.criteo.kafka.KafkaGangliaMetricsReporter
    kafka.ganglia.metrics.reporter.enabled=true

Here is a list of default properties used:

    kafka.ganglia.metrics.host=localhost
    kafka.ganglia.metrics.port=8649
    kafka.ganglia.metrics.group=kafka
    # This can be use to exclude some metrics from ganglia 
    # since kafka has quite a lot of metrics. The filter is
    # on MBeanName values. Enable the logger in RegexMetricPredicate
    # to see all the metrics available (~1000).
    # 
    kafka.ganglia.metrics.exclude.regex=<not set>

An example of filtered metrics :

    # To disable network metrics :
    kafka.ganglia.metrics.exclude.regex=^("kafka\.network".*)$

## Usage As Lib

Simply build the jar and publish it to your maven internal repository
(this package is not published to any public repositories
unfortunately).

  [GangliaReporter]: http://metrics.codahale.com/manual/ganglia/
