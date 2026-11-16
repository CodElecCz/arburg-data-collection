# Arburg Data Collection

Articles: [Česky](blog/index.cs.md) | [English](blog/index.en.md) | [Website](https://www.codelec.cz)

## Project overview

Arburg Data Collection is a Qt desktop application for reading production values from an Arburg machine over OPC UA and recording production events in a SQL database. It combines an OPC UA browser and live value view with a SQL browser, connection settings, and application logging.

The project is written in C++17 and uses Qt Widgets, Qt OPC UA, and Qt SQL. The main parts are:

- `opcua/OpcUaView.*` connects to the configured OPC UA server, browses its address space, reads selected nodes periodically, and handles connection state and reconnection.
- `opcua/OpcUaCheck.*` maps the selected production values and writes production records to the configured SQL table.
- `browser/` provides database connections and an SQL query view.
- `settings/` stores application and production-counter state; `log/` provides application logging.

The production mapping uses the configured Arburg values for item (`f052`), item description (`f052B`), good-piece counter (`f077`), reject counter (`f087`), job information (`f9007I`), and cycle time (`t085`). When the counters advance, the application records the corresponding piece-count delta and marks the row as good or rejected. Counter resets are handled as a new counter baseline.

## Build

Open `ArburgDataCollection.pro` in Qt Creator with a Qt installation that includes the Widgets, SQL, and OPC UA modules. Configure the OPC UA endpoint and SQL connection for the target installation before running the application.

## Articles

- [Project overview in Czech](blog/index.cs.md)
- [Project overview in English](blog/index.en.md)