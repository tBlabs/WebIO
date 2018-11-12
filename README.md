# BluePill

## Overview

```
+- BluePill board --------+
|                         |
|   (BluePill.Firmware)   |
|                         |
+-----------------+-------+
                  |
     Serial conn. |
     USB or UART  |
                  |
+- Host ----------+-------+
|                         |
|   (BluePill.Daemon)     |
|                         |
+-----------------+-------+
                  |
       Socket     |
       connection |
                  |
+- Client --------+-------+
|                         |
|  (BluePill.Client.Lib)  |
|            |            |
|            |            |
|         User App        |
|                         |
+-------------------------+
```

## Hardware

- [BluePill.Firmware](https://github.com/tBlabs/BluePill.Firmware) - firmware for board driving 

# Drivers

- [BluePill.Driver](https://github.com/tBlabs/BluePill.Driver) - highly configurable standalone host (with REST API and events generation ability)
- [BluePill.Daemon](https://github.com/tBlabs/BluePill.Daemon) - thin TCP host + board driver

# Daemon Clients

- [BluePill.Client.Lib](https://github.com/tBlabs/BluePill.Client.Lib) - base for other clients
- BluePill.Client.Cli (TODO)
- BluePill.Client.Http (TODO)

# Managers

- [FlowManager](https://github.com/tBlabs/EventsManager) - process manager for IoT devices
