# [NATS Streaming](https://nats.io): A high-performance cloud native messaging streaming system.

%%LOGO%%

`nats-streaming` is a high performance streaming server for the NATS Messaging System.

# Windows Docker images

Due to restrictions on how the Windows Docker Image is built, running the image without argument will run the NATS Streaming server with memory based store on port 4222 and the monitoring port 8222. If you need to specify any additional argument, or modify these options, you need to specify the executable name as this:

```bash
$ docker run -p 4223:4223 -p 8223:8223 %%IMAGE%% nats-streaming-server -p 4223 -m 8223
```

If you need to specify the entrypoint:

```bash
$ docker run --entrypoint c:/nats-streaming-server/nats-streaming-server -p 4222:4222 -p 8222:8222 %%IMAGE%%
```

# Non Windows Docker images

If you need to provide arguments to the NATS Streaming server, just pass them to the command line. For instance, to change the listen and monitoring port to 4223 and 8223 respectively:

```bash
$ docker run -p 4223:4223 -p 8223:8223 %%IMAGE%% -p 4223 -m 8223
```

If you need to specify the entrypoint:

```bash
$ docker run --entrypoint /nats-streaming-server -p 4222:4222 -p 8222:8222 %%IMAGE%%
```

# Example usage

```bash
# Run a NATS Streaming server
# Each server exposes multiple ports
# 4222 is for clients.
# 8222 is an HTTP management port for information reporting.
#
# To actually publish the ports when running the container, use the Docker port mapping
# flag "docker run -p <hostport>:<containerport>" to publish and map one or more ports,
# or the -P flag to publish all exposed ports and map them to high-order ports.
#
# This should not be confused with the NATS Streaming Server own -p parameter.
# For instance, to run the NATS Streaming Server and have it listen on port 4444,
# you would have to run like this:
#
#   docker run -p 4444:4444 %%IMAGE%% -p 4444
#
# Or, if you want to publish the port 4444 as a different port, for example 5555:
#
#   docker run -p 5555:4444 %%IMAGE%% -p 4444
#
# Check "docker run" for more information.

$ docker run -d -p 4222:4222 -p 8222:8222 %%IMAGE%%
```

Output that you would get if you had started with `-ti` instead of `d` (for daemon):

```bash
[1] 2019/04/16 21:24:11.886482 [INF] STREAM: Starting nats-streaming-server[test-cluster] version 0.14.0
[1] 2019/04/16 21:24:11.886524 [INF] STREAM: ServerID: mb87VWgNghJgoGnbRDWwQA
[1] 2019/04/16 21:24:11.886527 [INF] STREAM: Go version: go1.11.9
[1] 2019/04/16 21:24:11.886529 [INF] STREAM: Git commit: [218605a]
[1] 2019/04/16 21:24:11.886996 [INF] Starting nats-server version 1.4.1
[1] 2019/04/16 21:24:11.887058 [INF] Git commit [3e64f0b]
[1] 2019/04/16 21:24:11.887142 [INF] Starting http monitor on 0.0.0.0:8222
[1] 2019/04/16 21:24:11.887184 [INF] Listening for client connections on 0.0.0.0:4222
[1] 2019/04/16 21:24:11.887206 [INF] Server is ready
[1] 2019/04/16 21:24:11.915099 [INF] STREAM: Recovering the state...
[1] 2019/04/16 21:24:11.915131 [INF] STREAM: No recovered state
[1] 2019/04/16 21:24:12.166500 [INF] STREAM: Message store is MEMORY
[1] 2019/04/16 21:24:12.166576 [INF] STREAM: ---------- Store Limits ----------
[1] 2019/04/16 21:24:12.166582 [INF] STREAM: Channels:                  100 *
[1] 2019/04/16 21:24:12.166585 [INF] STREAM: --------- Channels Limits --------
[1] 2019/04/16 21:24:12.166618 [INF] STREAM:   Subscriptions:          1000 *
[1] 2019/04/16 21:24:12.166622 [INF] STREAM:   Messages     :       1000000 *
[1] 2019/04/16 21:24:12.166625 [INF] STREAM:   Bytes        :     976.56 MB *
[1] 2019/04/16 21:24:12.166629 [INF] STREAM:   Age          :     unlimited *
[1] 2019/04/16 21:24:12.166631 [INF] STREAM:   Inactivity   :     unlimited *
[1] 2019/04/16 21:24:12.166634 [INF] STREAM: ----------------------------------
```

To use a file based store instead, you would run:

```bash
$ docker run -d -p 4222:4222 -p 8222:8222 %%IMAGE%% -store file -dir datastore

[1] 2019/04/16 21:24:39.235166 [INF] STREAM: Starting nats-streaming-server[test-cluster] version 0.14.0
[1] 2019/04/16 21:24:39.235206 [INF] STREAM: ServerID: s9ulTmQAossdp4KKSA7jxT
[1] 2019/04/16 21:24:39.235209 [INF] STREAM: Go version: go1.11.9
[1] 2019/04/16 21:24:39.235211 [INF] STREAM: Git commit: [218605a]
[1] 2019/04/16 21:24:39.235865 [INF] Starting nats-server version 1.4.1
[1] 2019/04/16 21:24:39.235889 [INF] Git commit [3e64f0b]
[1] 2019/04/16 21:24:39.235949 [INF] Listening for client connections on 0.0.0.0:4222
[1] 2019/04/16 21:24:39.235973 [INF] Server is ready
[1] 2019/04/16 21:24:39.264025 [INF] STREAM: Recovering the state...
[1] 2019/04/16 21:24:39.264176 [INF] STREAM: No recovered state
[1] 2019/04/16 21:24:39.515371 [INF] STREAM: Message store is FILE
[1] 2019/04/16 21:24:39.515489 [INF] STREAM: Store location: datastore
[1] 2019/04/16 21:24:39.515562 [INF] STREAM: ---------- Store Limits ----------
[1] 2019/04/16 21:24:39.515604 [INF] STREAM: Channels:                  100 *
[1] 2019/04/16 21:24:39.515609 [INF] STREAM: --------- Channels Limits --------
[1] 2019/04/16 21:24:39.515612 [INF] STREAM:   Subscriptions:          1000 *
[1] 2019/04/16 21:24:39.515615 [INF] STREAM:   Messages     :       1000000 *
[1] 2019/04/16 21:24:39.515618 [INF] STREAM:   Bytes        :     976.56 MB *
[1] 2019/04/16 21:24:39.515620 [INF] STREAM:   Age          :     unlimited *
[1] 2019/04/16 21:24:39.515623 [INF] STREAM:   Inactivity   :     unlimited *
[1] 2019/04/16 21:24:39.515625 [INF] STREAM: ----------------------------------
```

You can also connect to a remote NATS Server running in a docker image. First, run NATS Server:

```bash
$ docker run -d --name=nats-main -p 4222:4222 -p 6222:6222 -p 8222:8222 nats
```

Now, start the Streaming server and link it to the above docker image:

```bash
$ docker run -d --link nats-main %%IMAGE%% -store file -dir datastore -ns nats://nats-main:4222

[1] 2019/04/16 21:24:56.168244 [INF] STREAM: Starting nats-streaming-server[test-cluster] version 0.14.0
[1] 2019/04/16 21:24:56.168321 [INF] STREAM: ServerID: bFaEuVz8Ak4J4Ga08lLFyW
[1] 2019/04/16 21:24:56.168327 [INF] STREAM: Go version: go1.11.9
[1] 2019/04/16 21:24:56.168331 [INF] STREAM: Git commit: [218605a]
[1] 2019/04/16 21:24:56.197393 [INF] STREAM: Recovering the state...
[1] 2019/04/16 21:24:56.197718 [INF] STREAM: No recovered state
[1] 2019/04/16 21:24:56.453938 [INF] STREAM: Message store is FILE
[1] 2019/04/16 21:24:56.453986 [INF] STREAM: Store location: datastore
[1] 2019/04/16 21:24:56.454021 [INF] STREAM: ---------- Store Limits ----------
[1] 2019/04/16 21:24:56.454025 [INF] STREAM: Channels:                  100 *
[1] 2019/04/16 21:24:56.454028 [INF] STREAM: --------- Channels Limits --------
[1] 2019/04/16 21:24:56.454030 [INF] STREAM:   Subscriptions:          1000 *
[1] 2019/04/16 21:24:56.454033 [INF] STREAM:   Messages     :       1000000 *
[1] 2019/04/16 21:24:56.454035 [INF] STREAM:   Bytes        :     976.56 MB *
[1] 2019/04/16 21:24:56.454039 [INF] STREAM:   Age          :     unlimited *
[1] 2019/04/16 21:24:56.454041 [INF] STREAM:   Inactivity   :     unlimited *
[1] 2019/04/16 21:24:56.454044 [INF] STREAM: ----------------------------------
```

Notice that the output shows that the NATS Server was not started, as opposed to the first output.

# Commandline Options

```bash
Streaming Server Options:
    -cid, --cluster_id  <string>         Cluster ID (default: test-cluster)
    -st,  --store <string>               Store type: MEMORY|FILE|SQL (default: MEMORY)
          --dir <string>                 For FILE store type, this is the root directory
    -mc,  --max_channels <int>           Max number of channels (0 for unlimited)
    -msu, --max_subs <int>               Max number of subscriptions per channel (0 for unlimited)
    -mm,  --max_msgs <int>               Max number of messages per channel (0 for unlimited)
    -mb,  --max_bytes <size>             Max messages total size per channel (0 for unlimited)
    -ma,  --max_age <duration>           Max duration a message can be stored ("0s" for unlimited)
    -mi,  --max_inactivity <duration>    Max inactivity (no new message, no subscription) after which a channel can be garbage collected (0 for unlimited)
    -ns,  --nats_server <string>         Connect to this external NATS Server URL (embedded otherwise)
    -sc,  --stan_config <string>         Streaming server configuration file
    -hbi, --hb_interval <duration>       Interval at which server sends heartbeat to a client
    -hbt, --hb_timeout <duration>        How long server waits for a heartbeat response
    -hbf, --hb_fail_count <int>          Number of failed heartbeats before server closes the client connection
          --ft_group <string>            Name of the FT Group. A group can be 2 or more servers with a single active server and all sharing the same datastore
    -sl,  --signal <signal>[=<pid>]      Send signal to nats-streaming-server process (stop, quit, reopen)
          --encrypt <bool>               Specify if server should use encryption at rest
          --encryption_cipher <string>   Cipher to use for encryption. Currently support AES and CHAHA (ChaChaPoly). Defaults to AES
          --encryption_key <sting>       Encryption Key. It is recommended to specify it through the NATS_STREAMING_ENCRYPTION_KEY environment variable instead

Streaming Server Clustering Options:
    --clustered <bool>                   Run the server in a clustered configuration (default: false)
    --cluster_node_id <string>           ID of the node within the cluster if there is no stored ID (default: random UUID)
    --cluster_bootstrap <bool>           Bootstrap the cluster if there is no existing state by electing self as leader (default: false)
    --cluster_peers <string, ...>        Comma separated list of cluster peer node IDs to bootstrap cluster state
    --cluster_log_path <string>          Directory to store log replication data
    --cluster_log_cache_size <int>       Number of log entries to cache in memory to reduce disk IO (default: 512)
    --cluster_log_snapshots <int>        Number of log snapshots to retain (default: 2)
    --cluster_trailing_logs <int>        Number of log entries to leave after a snapshot and compaction
    --cluster_sync <bool>                Do a file sync after every write to the replication log and message store
    --cluster_raft_logging <bool>        Enable logging from the Raft library (disabled by default)

Streaming Server File Store Options:
    --file_compact_enabled <bool>        Enable file compaction
    --file_compact_frag <int>            File fragmentation threshold for compaction
    --file_compact_interval <int>        Minimum interval (in seconds) between file compactions
    --file_compact_min_size <size>       Minimum file size for compaction
    --file_buffer_size <size>            File buffer size (in bytes)
    --file_crc <bool>                    Enable file CRC-32 checksum
    --file_crc_poly <int>                Polynomial used to make the table used for CRC-32 checksum
    --file_sync <bool>                   Enable File.Sync on Flush
    --file_slice_max_msgs <int>          Maximum number of messages per file slice (subject to channel limits)
    --file_slice_max_bytes <size>        Maximum file slice size - including index file (subject to channel limits)
    --file_slice_max_age <duration>      Maximum file slice duration starting when the first message is stored (subject to channel limits)
    --file_slice_archive_script <string> Path to script to use if you want to archive a file slice being removed
    --file_fds_limit <int>               Store will try to use no more file descriptors than this given limit
    --file_parallel_recovery <int>       On startup, number of channels that can be recovered in parallel
    --file_truncate_bad_eof <bool>       Truncate files for which there is an unexpected EOF on recovery, dataloss may occur

Streaming Server SQL Store Options:
    --sql_driver <string>            Name of the SQL Driver ("mysql" or "postgres")
    --sql_source <string>            Datasource used when opening an SQL connection to the database
    --sql_no_caching <bool>          Enable/Disable caching for improved performance
    --sql_max_open_conns <int>       Maximum number of opened connections to the database

Streaming Server TLS Options:
    -secure <bool>                   Use a TLS connection to the NATS server without
                                     verification; weaker than specifying certificates.
    -tls_client_key <string>         Client key for the streaming server
    -tls_client_cert <string>        Client certificate for the streaming server
    -tls_client_cacert <string>      Client certificate CA for the streaming server

Streaming Server Logging Options:
    -SD, --stan_debug=<bool>         Enable STAN debugging output
    -SV, --stan_trace=<bool>         Trace the raw STAN protocol
    -SDV                             Debug and trace STAN
         --syslog_name               On Windows, when running several servers as a service, use this name for the event source
    (See additional NATS logging options below)

Embedded NATS Server Options:
    -a, --addr <string>              Bind to host address (default: 0.0.0.0)
    -p, --port <int>                 Use port for clients (default: 4222)
    -P, --pid <string>               File to store PID
    -m, --http_port <int>            Use port for http monitoring
    -ms,--https_port <int>           Use port for https monitoring
    -c, --config <string>            Configuration file

Logging Options:
    -l, --log <string>               File to redirect log output
    -T, --logtime=<bool>             Timestamp log entries (default: true)
    -s, --syslog <string>            Enable syslog as log method
    -r, --remote_syslog <string>     Syslog server addr (udp://localhost:514)
    -D, --debug=<bool>               Enable debugging output
    -V, --trace=<bool>               Trace the raw protocol
    -DV                              Debug and trace

Authorization Options:
        --user <string>              User required for connections
        --pass <string>              Password required for connections
        --auth <string>              Authorization token required for connections

TLS Options:
        --tls=<bool>                 Enable TLS, do not verify clients (default: false)
        --tlscert <string>           Server certificate file
        --tlskey <string>            Private key for server certificate
        --tlsverify=<bool>           Enable TLS, verify client certificates
        --tlscacert <string>         Client certificate CA for verification

NATS Clustering Options:
        --routes <string, ...>       Routes to solicit and connect
        --cluster <string>           Cluster URL for solicited routes

Common Options:
    -h, --help                       Show this message
    -v, --version                    Show version
        --help_tls                   TLS help.
```

# Configuration

Details on how to configure further the NATS Streaming server can be found [here](https://github.com/nats-io/nats-streaming-server#configuring)
