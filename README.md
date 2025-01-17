# ETA Override

The best ETA in 3d printing is ETA comming from slicer software. Slicer adds M73 commands
with estimations of print progress, time, time until next pause etc.

This plugin uses firmware reports issued to serial output and comming from M73 g-code commands.
Supported firmware issues M73 Reports for SD-card and USB printing.

Data used by plugin:
* time until end of printing
* time progress reflected in OctoPrint web UI progress bar
  (but due to OctoPrint limitations not in API, see https://github.com/OctoPrint/OctoPrint/issues/4663)

Also this plugin queries for position (M114) when every M73 command parsing happens and fires z-change event
(to support sending status message every X milimeters via telegram).

## Supported firmware

Supported firmware list and recognized messages.

* [Prusa Firmware](https://github.com/prusa3d/Prusa-Firmware) (v3.3.0+)

```
NORMAL MODE: Percent done: 21; print time remaining in mins: 33
SILENT MODE: Percent done: 21; print time remaining in mins: 34
```

```
NORMAL MODE: Percent done: 21; print time remaining in mins: 33; Change in mins: -1
SILENT MODE: Percent done: 21; print time remaining in mins: 34; Change in mins: -1
```

* [Marlin 2](https://github.com/MarlinFirmware/Marlin) (v2.1.2+)

```
echo:  M73 Percent done: 10; Print time remaining in mins: 20; Change in mins: 7;
```

but also other variant (when default M73_REPORT_PRUSA option is disabled)

```
echo:  M73 Progress: 10%; Time left: 20.0m; Change: 7m
```

(each part of report is optional and configurable in Marlin 2)


## Setup

Install via the bundled Plugin Manager or manually using this URL:

    https://github.com/arekm/octopi_eta_override/archive/master.zip

## Develop

Setup environment the same way as for OctoPrint development:

https://docs.octoprint.org/en/master/development/environment.html

(installation; once)
```
pre-commit install
```

(formatting checking)
```
pre-commit run --hook-stage manual --all-files
```

(run tests)
```
pytest
```
