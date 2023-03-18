# Pika Metric Exporter

## Pika Metrics Definition

### Pika Server Info

| Metrics Name                | Metric Type | Labels                                                                                                          | Metrics Value                    | Metric Desc                                                            |
| --------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------- | ---------------------------------------------------------------------- |
| namespace_build_info        | `Gauge`     | {addr="", alias="", "os"="", "arch_bits"="", "pika_version"="", "pika_git_sha"="","pika_build_compile_date"=""} | 1                                | pika binary file build info                                            |
| namespace_server_info       | `Gauge`     | {addr="", alias="", "process_id"="", "tcp_port"="", "config_file"="", "server_id"="", "role"=""}                | 1                                | pika instance's info, the label `role` is the role in replication info |
| namespace_uptime_in_seconds | `Gauge`     | {addr="", alias=""}                                                                                             | the value of `uptime_in_seconds` | pika instance's uptime in seconds                                      |
| namespace_thread_num        | `Gauge`     | {addr="", alias=""}                                                                                             | the value of `thread_num`        | pika instance's thread num                                             |
| namespace_sync_thread_num   | `Gauge`     | {addr="", alias=""}                                                                                             | the value of `sync_thread_num`   | pika instance's thread num for syncing                                 |

### Pika Data Info

| Metrics Name                   | Metric Type | Labels                                | Metrics Value                       | Metric Desc                                                                                                                                                                                             |
| ------------------------------ | ----------- | ------------------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| namespace_db_size              | `Gauge`     | {addr="", alias="", "compression"=""} | the value of `db_size`              | total db data size (in bytes) of the pika instance, statistics of all files under the configured `db-path`                                                                                              |
| namespace_log_size             | `Gauge`     | {addr="", alias=""}                   | the value of `log_size`             | total log data size (in bytes) of the pika instance, statistics of all files under the configured `log-path` witch contains INFO, WARNING, ERROR logs and binlog (write2fine) files for synchronization |
| namespace_used_memory          | `Gauge`     | {addr="", alias=""}                   | the value of `used_memory`          | total used memory size (in bytes) of the pika instance                                                                                                                                                  |
| namespace_db_memtable_usage    | `Gauge`     | {addr="", alias=""}                   | the value of `db_memtable_usage`    | total memtable used memory size (in bytes) of the pika instance                                                                                                                                         |
| namespace_db_tablereader_usage | `Gauge`     | {addr="", alias=""}                   | the value of `db_tablereader_usage` | total tablereader used memory size (in bytes) of the pika instance                                                                                                                                      |
| namespace_db_fatal             | `Gauge`     | {addr="", alias=""}                   | the value of `db_fatal`             | the metrics value: 1 means errors occurred, 0 means no error                                                                                                                                            |

### Pika Clients Info

| Metrics Name                | Metric Type | Labels              | Metrics Value                    | Metric Desc                                       |
| --------------------------- | ----------- | ------------------- | -------------------------------- | ------------------------------------------------- |
| namespace_connected_clients | `Gauge`     | {addr="", alias=""} | the value of `connected_clients` | total count of connected clients in pika instance |

### Pika Stats Info

| Metrics Name                         | Metric Type | Labels                                                       | Metrics Value                             | Metric Desc                                                                           |
| ------------------------------------ | ----------- | ------------------------------------------------------------ | ----------------------------------------- | ------------------------------------------------------------------------------------- |
| namespace_total_connections_received | `Counter`   | {addr="", alias=""}                                          | the value of `total_connections_received` | total count of received connections from clients in pika instance                     |
| namespace_instantaneous_ops_per_sec  | `Gauge      | {addr="", alias=""}                                          | the value of `instantaneous_ops_per_sec`  | the count of prcessed operations in per seconds by pika instance                      |
| namespace_total_commands_processed   | `Counter`   | {addr="", alias=""}                                          | the value of `total_commands_processed`   | total count of processed commands in pika instance                                    |
| namespace_is_bgsaving                | `Gauge`     | {addr="", alias=""}                                          | 0 or 1                                    | the metrics value: 1 means bgsave is in progress, 0 means bgsave is not in progress   |
| namespace_is_scaning_keyspace        | `Gauge`     | {addr="", alias=""}                                          | 0 or 1                                    | the metrics value: 1 means the keyspace is scanning, 0 means not scanning             |
| namespace_compact                    | `Gauge`     | {addr="", alias="", compact_cron"="", "compact_interval":""} | 0 or 1                                    | the metrics value: 1 means compact is in progress, 0 means compact is not in progress |

### Pika Command Exec Count Info

| Metrics Name                 | Metric Type | Labels                            | Metrics Value                           | Metric Desc                                         |
| ---------------------------- | ----------- | --------------------------------- | --------------------------------------- | --------------------------------------------------- |
| namespace_command_exec_count | `Counter`   | {addr="", alias="", "command"=""} | the value of the command executed count | the count of each command executed in pika instance |

### Pika CPU Info

| Metrics Name                     | Metric Type | Labels              | Metrics Value                         | Metric Desc                                                        |
| -------------------------------- | ----------- | ------------------- | ------------------------------------- | ------------------------------------------------------------------ |
| namespace_used_cpu_user_children | `Counter`   | {addr="", alias=""} | the value of `used_cpu_user_children` | total user CPU usage time (in seconds) of pika children instance   |
| namespace_used_cpu_user          | `Counter`   | {addr="", alias=""} | the value of `used_cpu_user`          | total user CPU usage time (in seconds) of pika instance            |
| namespace_used_cpu_sys_children  | `Counter`   | {addr="", alias=""} | the value of `used_cpu_sys_children`  | total system CPU usage time (in seconds) of pika children instance |
| namespace_used_cpu_sys           | `Counter`   | {addr="", alias=""} | the value of `used_cpu_sys`           | total system CPU usage time (in seconds) of pika instance          |

### Pika Replication Info

| Metrics Name                       | Metric Type | Labels                                                                                   | Metrics Value                                | Metric Desc                                                                                                   |
| ---------------------------------- | ----------- | ---------------------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| namespace_connected_slaves         | `Gauge`     | {addr="", alias=""}                                                                      | the value of `connected_slaves`              | the count of connected slaves, when pika instance's role is master                                            |
| namespace_partition_slave_lag      | `Gauge`     | {addr="", alias="", "slave_conn_fd"="", slave_ip"="", "slave_port"="", "partition"=""}   | parse master `slave info's lag`              | the binlog lag of all slaves of the pika instance                                                             |
| namespace_master_link_status       | `Gauge`     | {addr="", alias="", "master_host"="", "master_port"=""}                                  | 0 or 1                                       | connection state between slave and master(1 means all partitions sync ok), when pika instance's role is slave |
| namespace_slave_read_only          | `Gauge`     | {addr="", alias="", "master_host"="", "master_port"=""}                                  | 0 or 1                                       | is slave read only, when pika instance's role is slave                                                        |
| namespace_slave_priority           | `Gauge`     | {addr="", alias="", "master_host"="", "master_port"=""}                                  | the value of `slave_priority`                | slave priority, when pika instance's role is slave                                                            |
| namespace_partition_repl_state     | `Gauge`     | {addr="", alias="", "master_host"="", "master_port"="", "partition"="", "repl_state"=""} | 0                                            | sync connection state between slave and master for each partition, when pika instance's role is slave         |
| namespace_db_binlog_offset_filenum | `Gauge`     | {addr="", alias="", "db"=""}                                                             | the value of `binlog_offset filenum` each db | binlog file num for each db                                                                                   |
| namespace_db_binlog_offset         | `Gauge`     | {addr="", alias="", "db"="", "safety_purge"=""}                                          | the value of `binlog_offset offset` each db  | binlog offset for each db                                                                                     |
| namespace_db_consensus_last_log    | `Gauge`     | {addr="", alias="", "db"="", "last_log"=""}                                              | the value of `consensus last_log` each db    | consensus last_log for each db when consensus-level is enabled                                                |

### Pika Keyspace Info

| Metrics Name                       | Metric Type | Labels                                  | Metrics Value                                        | Metric Desc                                                   |
| ---------------------------------- | ----------- | --------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------- |
| namespace_keyspace_last_start_time | `Gauge`     | {addr="", alias=""}                     | the value of `Keyspace Time` convert to unix seconds | the start time(unix seconds) of the last statistical keyspace |
| namespace_keys                     | `Gauge`     | {addr="", alias="", "db"="", "type"=""} | the value of `keys`                                  | total count of the key-type keys for each db                  |
| namespace_expire_keys              | `Gauge`     | {addr="", alias="", "db"="", "type"=""} | the value of `expire_keys`                           | total count of the key-type expire keys for each db           |
| namespace_invalid_keys             | `Gauge`     | {addr="", alias="", "db"="", "type"=""} | the value of `invalid_keys`                          | total count of the key-type invalid keys for each db          |

### Pika Command Execution Time

### Rocksdb Metrics
