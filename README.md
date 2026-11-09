<div align="center">
    <p align="center">
        <a align="center" href="https://docs.kernel.org/trace/events.html">
          <img width="5%" src="https://github.com/cybersecurity-dev/cybersecurity-dev/blob/main/assets/Tux.svg" />
        </a>
    </p>

```mermaid
flowchart TB
    subgraph Sources["Linux Event Sources"]
        direction LR
        APP["User-Space Applications"]
        PROC["Processes and Threads"]
        FILE["File-System Operations"]
        NET["Network Activity"]
        SYS["System Calls"]
        KERN["Kernel Events"]
    end

    subgraph Instrumentation["Tracing and Instrumentation Layer"]
        direction LR
        TP["Kernel Tracepoints"]
        KP["Kprobes / Kretprobes"]
        UP["Uprobes / Uretprobes"]
        PERF["Perf Events"]
        LSM["eBPF LSM Hooks"]
    end

    subgraph Collection["Event Collection Layer"]
        EBPF["eBPF Programs"]
        MAPS["eBPF Maps"]
        BUFFER["Ring Buffer / Perf Buffer"]
        LOADER["User-Space eBPF Loader"]
    end

    subgraph Processing["Event Processing Pipeline"]
        INGEST["Event Ingestion"]
        PARSE["Parsing and Normalization"]
        ENRICH["Context Enrichment<br/>PID, UID, container, namespace"]
        FILTER["Filtering and Aggregation"]
        CORRELATE["Event Correlation"]
        FEATURE["Graph and Feature Construction"]
    end

    subgraph Detection["Analysis and Detection"]
        RULES["Rule-Based Detection"]
        ML["Machine-Learning Model"]
        CPG["Code Property Graph Analysis"]
        BEHAVIOR["Behavioral Analysis"]
        ALERT["Alert Generation"]
    end

    subgraph Storage["Storage Layer"]
        EVENTDB[("Event Database")]
        GRAPHDB[("Graph Database")]
        LOGS[("Raw Event Archive")]
    end

    subgraph Presentation["Management and Visualization"]
        API["REST / gRPC API"]
        DASH["Monitoring Dashboard"]
        QUERY["Investigation Interface"]
        REPORT["Reports and Exports"]
        SIEM["SIEM Integration"]
    end

    Sources --> Instrumentation

    TP --> EBPF
    KP --> EBPF
    UP --> EBPF
    PERF --> EBPF
    LSM --> EBPF

    LOADER -->|Load and configure| EBPF
    EBPF --> MAPS
    MAPS --> BUFFER
    BUFFER --> LOADER
    LOADER --> INGEST

    INGEST --> PARSE
    PARSE --> ENRICH
    ENRICH --> FILTER
    FILTER --> CORRELATE
    CORRELATE --> FEATURE

    FEATURE --> RULES
    FEATURE --> ML
    FEATURE --> CPG
    FEATURE --> BEHAVIOR

    RULES --> ALERT
    ML --> ALERT
    CPG --> ALERT
    BEHAVIOR --> ALERT

    PARSE --> LOGS
    ENRICH --> EVENTDB
    FEATURE --> GRAPHDB

    EVENTDB --> API
    GRAPHDB --> API
    LOGS --> API
    ALERT --> API

    API --> DASH
    API --> QUERY
    API --> REPORT
    API --> SIEM

    classDef source fill:#e8f1ff,stroke:#2563eb,color:#172554
    classDef trace fill:#ede9fe,stroke:#7c3aed,color:#2e1065
    classDef collect fill:#dcfce7,stroke:#16a34a,color:#052e16
    classDef process fill:#fef3c7,stroke:#d97706,color:#451a03
    classDef detect fill:#fee2e2,stroke:#dc2626,color:#450a0a
    classDef storage fill:#e0f2fe,stroke:#0284c7,color:#082f49
    classDef view fill:#f3e8ff,stroke:#9333ea,color:#3b0764

    class APP,PROC,FILE,NET,SYS,KERN source
    class TP,KP,UP,PERF,LSM trace
    class EBPF,MAPS,BUFFER,LOADER collect
    class INGEST,PARSE,ENRICH,FILTER,CORRELATE,FEATURE process
    class RULES,ML,CPG,BEHAVIOR,ALERT detect
    class EVENTDB,GRAPHDB,LOGS storage
    class API,DASH,QUERY,REPORT,SIEM view
```

# **`LET`** | _Event Tracing for Linux_
> LET is a tracing facility that allows a user to log events to a file (_JSON, XML, CSV_)
</div>

[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)]()
[![YouTube](https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white)]()
[![Reddit](https://img.shields.io/badge/Reddit-FF4500?style=for-the-badge&logo=reddit&logoColor=white)]()

<p align="center">
    <a href="https://github.com/cybersecurity-dev/"><img height="25" src="https://github.com/cybersecurity-dev/cybersecurity-dev/blob/main/assets/github.svg" alt="GitHub"></a>
    &nbsp;
    <a href="https://www.youtube.com/@CyberThreatDefence"><img height="25" src="https://github.com/cybersecurity-dev/cybersecurity-dev/blob/main/assets/youtube.svg" alt="YouTube"></a>
    &nbsp;
    <a href="https://cyberthreatdefence.com/my_awesome_lists"><img height="20" src="https://github.com/cybersecurity-dev/cybersecurity-dev/blob/main/assets/blog.svg" alt="My Awesome Lists"></a>
    <img src="https://github.com/cybersecurity-dev/cybersecurity-dev/blob/main/assets/bar.gif">
</p>

[![Linux](https://img.shields.io/badge/Linux-Supported-brightgreen?logo=linux&logoColor=white)](https://github.com/cybersecurity-dev/LET)

```mermaid
flowchart LR
    A["Linux System<br/>Processes, Files, Network"]
    B["Event Tracing<br/>eBPF / Tracepoints"]
    C["Event Collector"]
    D["Event Processing<br/>Parse and Filter"]
    E[("Event Storage")]
    F["Dashboard and Analysis"]
    G["Alerts"]

    A -->|Generate events| B
    B -->|Capture events| C
    C --> D
    D --> E
    E --> F
    D -->|Suspicious activity| G

    classDef system fill:#DBEAFE,stroke:#2563EB,color:#172554
    classDef tracing fill:#EDE9FE,stroke:#7C3AED,color:#2E1065
    classDef processing fill:#FEF3C7,stroke:#D97706,color:#451A03
    classDef storage fill:#DCFCE7,stroke:#16A34A,color:#052E16
    classDef output fill:#FEE2E2,stroke:#DC2626,color:#450A0A

    class A system
    class B,C tracing
    class D processing
    class E storage
    class F,G output
```

## 📖 Contents
- [Installation Steps](#installation-steps)
- [My Awesome Lists](#my-awesome-lists)
- [Contributing](#contributing)
- [Contributors](#contributors)

## Installation Steps

<details>

<summary>Install required tools on Linux</summary>

### For Ubuntu 18.04, 20.04, 22.04

```bash
sudo apt-get update
sudo apt-get install -y libtraceevent-dev \
                        libtracefs-dev
```
</details>

<details>

<summary>Install required python libs</summary>

### pip install
```bash
pip install -r requirements.txt
python3 setup.py install
```

### conda install
```bash
conda config --add channels conda-forge
conda install --file requirements_conda.txt
python3 setup.py install
```

</details>

## Common Linux Kernel Event Types

| **Event Type**       | **Description**                                                             | **Subsystem / Use Case**           |
|----------------------|------------------------------------------------------------------------------|------------------------------------|
| `IN_ACCESS`          | File was accessed                                                           | inotify                            |
| `IN_MODIFY`          | File was modified                                                           | inotify                            |
| `IN_ATTRIB`          | Metadata changed (e.g., permissions, timestamps)                            | inotify                            |
| `IN_CLOSE_WRITE`     | File opened for writing was closed                                          | inotify                            |
| `IN_CLOSE_NOWRITE`   | File not opened for writing was closed                                      | inotify                            |
| `IN_OPEN`            | File was opened                                                             | inotify                            |
| `IN_MOVED_FROM`      | File moved out of watched directory                                         | inotify                            |
| `IN_MOVED_TO`        | File moved into watched directory                                           | inotify                            |
| `IN_CREATE`          | File/directory created in watched directory                                 | inotify                            |
| `IN_DELETE`          | File/directory deleted in watched directory                                 | inotify                            |
| `IN_DELETE_SELF`     | Watched file/directory was itself deleted                                   | inotify                            |
| `IN_MOVE_SELF`       | Watched file/directory was itself moved                                     | inotify                            |
| `EPOLLIN`            | File descriptor is ready for read                                           | epoll                              |
| `EPOLLOUT`           | File descriptor is ready for write                                          | epoll                              |
| `EPOLLERR`           | Error condition on file descriptor                                          | epoll                              |
| `EPOLLHUP`           | Hang up happened on the associated file descriptor                          | epoll                              |
| `FAN_ACCESS`         | File was accessed                                                           | fanotify                           |
| `FAN_MODIFY`         | File was modified                                                           | fanotify                           |
| `FAN_CLOSE_WRITE`    | Writable file was closed                                                    | fanotify                           |
| `FAN_CLOSE_NOWRITE`  | Unwritable file was closed                                                  | fanotify                           |
| `FAN_OPEN`           | File was opened                                                             | fanotify                           |
| `FAN_EVENT_ON_CHILD` | Events occurred on a child of the watched directory                         | fanotify                           |
| `KEY_PRESS`          | Key was pressed                                                             | input subsystem (`/dev/input`)     |
| `KEY_RELEASE`        | Key was released                                                            | input subsystem (`/dev/input`)     |
| `REL_X`, `REL_Y`     | Relative mouse movement                                                     | input subsystem                    |
| `ABS_X`, `ABS_Y`     | Absolute pointer position                                                   | input subsystem                    |
| `AUDIT_SYSCALL`      | System call event                                                           | auditd / kernel audit subsystem    |
| `NETLINK_ROUTE`      | Network interface changes (e.g., link up/down)                              | netlink                            |


##

### My Awesome Lists
You can access the my awesome lists [here](https://cyberthreatdefence.com/my_awesome_lists)

### Contributing

[Contributions of any kind welcome, just follow the guidelines](contributing.md)!

### Contributors

[Thanks goes to these contributors](https://github.com/cybersecurity-dev/LET/graphs/contributors)!

[🔼 Back to top](#let--event-tracing-for-linux)
