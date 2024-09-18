# Bluefors log plotting tool

## Overview

This tool reads and processes log files from a specified directory and date range, extracting various types of log data such as temperature, pressure, flow rate, and more. It then visualizes the data using plots, making it easy to analyze system performance over time. The log files are assumed to be stored in separate folders by date, and each folder contains multiple log files of different types (e.g., channel logs, status logs, flowmeter logs).

The tool supports log files that follow a specific format, including but not limited to the following types:
- Channel (temperature) logs
- Status logs
- Flowmeter logs
- Maxigauge (pressure) logs
- Heater logs

The code can be executed via the command line, where the user specifies the log file directory and the date range to be analyzed.

## Features

- **Log Type Processing:** Automatically identifies and processes various log file types based on their file names.
- **Date Range Filtering:** Allows filtering of log data based on a single date or a date range.
- **Data Processing:** Reads log data, formats it into dataframes, and indexes it by timestamp.
- **Visualization:** Generates time-series plots of the processed log data.
- **Extensibility:** Can easily be extended to support new log formats and data types.

## Requirements

- Python 3.7+
- Required libraries:
  - `os`
  - `argparse`
  - `re`
  - `pandas`
  - `matplotlib`
  - `datetime`
  - `collections`
  - `StringIO` (from `io`)

You can install the required libraries using:

```bash
pip install pandas matplotlib
```

## Usage

Run the script from the command line with the following arguments:

```bash
python log_plotting_tool.py <log_path> <start_date> [end_date]
```

### Arguments:
- `log_path` (str): Path to the directory containing the log files.
- `start_date` (str): Start date to filter log files, in the format `YY-MM-DD`.
- `[end_date]` (str, optional): Optional end date to filter log files. If not provided, the tool processes only the logs from the `start_date`.

### Example:

```bash
python log_plotting_tool.py ./logs 23-09-15 23-09-16
```

This example will read log files from the `./logs` directory for the dates September 15, 2023, and September 16, 2023.

### Output:

The tool will plot graphs of relevant data such as:
- **Temperature** (from channel logs)
- **Pressure** (from Maxigauge logs)
- **Flowrate** (from Flowmeter logs)

The plots will display different channels using distinct colors and labels for easy identification. 

## Log File Format

### Supported Log Types:
1. **CH (Channel) Logs**: Logs containing temperature data for different channels (e.g., CH1, CH2, CH5, CH6).
   - Format: `<Date>,<Time>,<Temperature>`
   - Example filename: `CH1_T_23-09-15.log`

2. **Status Logs**: Logs containing status information in key-value pairs.
   - Format: `<Date>,<Time>,<Label1>,<Value1>,<Label2>,<Value2>,...`
   - Example filename: `Status_23-09-15.log`

3. **Flowmeter Logs**: Logs with flow rate data.
   - Format: `<Date>,<Time>,<Flowrate>`
   - Example filename: `Flowmeter_23-09-15.log`

4. **Maxigauge Logs**: Logs with pressure readings for various sensors (P1, P2, ..., P6).
   - Format: `<Date>,<Time>,<Label1>,<Value1>,...`
   - Example filename: `maxigauge_23-09-15.log`

5. **Heater Logs**: Logs containing information about heater states.
   - Format: `<Date>,<Time>,<Heater1>,<Heater2>,...`
   - Example filename: `Heaters_23-09-15.log`

## Extending the Tool

To add support for additional log types, follow these steps:
1. Define a new `process_<log_type>_logs` function to handle the specific log format.
2. Add the new log type in the `process_combined_data_by_type` function.
3. Ensure the new log type is identified properly in the `identify_log_type` function.

## License

This tool is provided as open-source software. You are free to use, modify, and distribute it as needed.
