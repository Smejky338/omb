Users can deploy the helm chart:

```bash
$ helm install ./benchmark --name benchmark
```

After the chart has started, users can exec into the pod name "benchmark-driver" and run the benchmark from there.

For example, once inside the "benchmark-driver" pod, users can execute:

```bash
bin/benchmark --drivers driver-pulsar/pulsar.yaml --workers $WORKERS workloads/1-topic-16-partitions-1kb.yaml
```

All workers that has configured to startup will be set in the "$WORKERS" env variable

To tear down the chart:

```bash
$ helm delete benchmark --purge
```
## Perfscale use on MSK Kafka

### Install

```
oc new-project cpt-benchmark-msk
helm install benchmark-omb deployment/kubernetes/helm/benchmark -n cpt-benchmark-msk
```

### Use

From the shell of driver:

```bash
bin/benchmark --drivers driver-kafka/kafka-throughput.yaml --workers $WORKERS workloads/1-topic-16-partitions-1kb.yaml
benchmark-omb-worker.cpt-benchmark-msk.svc.cluster.local

bin/benchmark --drivers driver-kafka/kafka-big-batches-gzip.yaml --workers $WORKERS workloads/1-topic-16-partitions-1kb.yaml
benchmark-omb-worker.cpt-benchmark-msk.svc.cluster.local
```

bin/benchmark --drivers driver-kafka/kafka.yaml --workers $WORKERS workloads/1-topic-16-partitions-1kb.yaml

### Delete
```
helm delete benchmark-omb
```
