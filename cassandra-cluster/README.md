# Cassandra & Monk

This repository contains Monk.io template to deploy Cassandra & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

### Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository

```bash
git clone https://github.com/monk-io/cassandra-cluster
```

## Load Template

```bash
cd cassandra-cluster
monk load MANIFEST
```

### Let's take a look at the themes I have installed

```bash
foo@bar:~$ monk list cassandra-cluster
✔ Got the list
Type      Template                   Repository  Version  Tags
runnable  cassandra-cluster/cassandra1  local       -        -
runnable  cassandra-cluster/cassandra2  local       -        -
group     cassandra-cluster/stack       local       -        -

```

## Deploy Stack

```bash
foo@bar:~$ monk run cassandra-cluster/stack
? Select tag to run [local/cassandra-cluster/stack] on: monk
✔ Starting the job: local/cassandra-cluster/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% bitnami/cassandra:latest monk-1
✔ [================================================] 100% bitnami/cassandra:latest monk-2
✔ Checking/pulling images DONE
✔ Started local/cassandra-cluster/stack

🔩 templates/local/cassandra-cluster/stack
 ├─🧊 Peer monk-2
 │  └─🔩 templates/local/cassandra-cluster/cassandra1
 │     └─📦 117f280606b2d3ab4544e229e2b52a60-ndra-cassandra1-cassandra-cluster
 │        ├─🧩 bitnami/cassandra:latest
 │        ├─💾 /var/lib/monkd/volumes/cassandra/cassandra1 -> /bitnami
 │        └─🔌 open <ip>:9042 (0.0.0.0:9042) -> 9042
 └─🧊 Peer monk-1
    └─🔩 templates/local/cassandra-cluster/cassandra2
       └─📦 67e8de9c4531e95d7cd1698941819d78-ndra-cassandra2-cassandra-cluster
          ├─🧩 bitnami/cassandra:latest
          ├─💾 /var/lib/monkd/volumes/cassandra/cassandra2 -> /bitnami
          └─🔌 open <ip>:9043 (0.0.0.0:9043) -> 9042

💡 You can inspect and manage your above stack with these commands:
 monk logs (-f) local/cassandra-cluster/stack - Inspect logs
 monk shell     local/cassandra-cluster/stack - Connect to the container's shell
 monk do        local/cassandra-cluster/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Variables

The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable           | Description                           | Default |
| ------------------ | ------------------------------------- | ------- |
| cassandra-password | cassandra password, Default: monk     | monk    |
| cassandra-cluster  | Cassandra cluster name, Default: monk | monk    |

## Stop, remove and clean up workloads and templates

```bash
monk purge cassandra-cluster
```
