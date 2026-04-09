# TwinSpark8s – Experiment Data

Experiment data from evaluating two 1-out-of-2 (1oo2) Kubernetes high-availability configurations on 2-node clusters using the TwinSpark8s fault injection framework.

## Configurations Tested

- **etcd/DRBD/keepalived**: Single external etcd instance replicated via DRBD with keepalived-managed virtual IP failover.
- **MySQL/Kine/HAProxy**: MySQL master-master replication with HAProxy routing and Kine as etcd shim for k3s.

## Failure Types

- **Node Crash**: Network interface taken down, k3s stopped, server rebooted.
- **Network Partition**: Inter-node traffic blocked; external traffic unaffected.

Each scenario was run 20 times. Failover and failback phases are measured separately.

## Metrics

| Metric | Description |
|--------|-------------|
| Total Requests | Requests sent to the WebSocket service |
| Successful / Failed Requests | Breakdown of request outcomes |
| Avg Response Time (ms) | Average client-observed response latency |
| Recovery Time (ms) | Duration of client-side service unavailability |
| K8s API Failure Checks / API Failures | API health check count and failure count |
| K8s API Unavailable Time (ms) | Duration the Kubernetes API was unreachable |
| K8s API Availability (%) | Fraction of measurement time with API reachable |

## Data Files

| File | Configuration | Failure Type |
|------|---------------|--------------|
| `experiment_data/experiment_results_crash_etcd.md` | etcd/DRBD/keepalived | Node Crash |
| `experiment_data/experiment_results_crash_mysql.md` | MySQL/Kine/HAProxy | Node Crash |
| `experiment_data/experiment_results_partition_etcd.md` | etcd/DRBD/keepalived | Network Partition |
| `experiment_data/experiment_results_partition_mysql.md` | MySQL/Kine/HAProxy | Network Partition |

Each file contains per-run results and summary statistics (mean, median, min, max, std dev).
