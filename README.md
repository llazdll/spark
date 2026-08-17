# BusyMonth — Spark Project

## Overview

This project uses **Apache Spark (PySpark)** to analyze the `lax_passengers.csv` dataset and identify the busiest months at Los Angeles International Airport (LAX).

The goal is to find every month in which the **combined number of passengers** traveling through:

* Terminal 1
* Terminal 2
* Terminal 3
* Terminal 4
* Terminal 5
* Terminal 6
* Terminal 7
* Terminal 8
* Tom Bradley International Terminal

is **greater than 5,000,000 passengers**.

## Dataset

The input dataset is:

```text
lax_passengers.csv
```

Important columns:

| Column                   | Description                       |
| ------------------------ | --------------------------------- |
| `DataExtractDate`        | Date when the data was extracted  |
| `ReportPeriod`           | Reporting month                   |
| `Terminal`               | Airport terminal                  |
| `Arrival_Departure`      | Arrival or departure              |
| `Domestic_International` | Domestic or international traffic |
| `Passenger_Count`        | Number of passengers              |

The `ReportPeriod` values use the following format:

```text
MM/dd/yyyy hh:mm:ss a
```

For example:

```text
01/01/2006 12:00:00 AM
```

The project converts this into a month/year format:

```text
01/2006
```

## Approach

The Spark program performs the following operations:

1. Read `lax_passengers.csv`.
2. Select only the required terminals.
3. Convert `ReportPeriod` into a usable date/time value.
4. Extract the month and year.
5. Group records by month.
6. Sum `Passenger_Count` for each month.
7. Keep only months where the total is greater than 5,000,000.
8. Display the month and total passenger count.

Conceptually:

```text
lax_passengers.csv
        ↓
Filter required terminals
        ↓
Convert ReportPeriod
        ↓
Extract Month/Year
        ↓
GROUP BY Month
        ↓
SUM(Passenger_Count)
        ↓
Total > 5,000,000
        ↓
Busy Months
```

## Expected Output

The final output follows this format:

```text
01/2006    5,001,008
08/2006    6,000,134
...
```

Each row represents a month whose combined passenger count exceeded five million.

## Technologies

* Python
* PySpark
* Apache Spark
* Google Colab

## Project Structure

```text
.
├── BusyMonth.py
├── lax_passengers.csv
└── README.md
```

> **Note:** If the dataset should not be publicly redistributed, keep `lax_passengers.csv` out of the Git repository and add it to `.gitignore`.

## Running the Project

### Using Google Colab

Install or use an environment with PySpark available, upload the dataset, and run the `BusyMonth.py` program.

### Using a local Spark environment

Run:

```bash
spark-submit BusyMonth.py
```

## Learning Objective

This project demonstrates fundamental Spark data-processing operations, including:

* Reading CSV data
* Filtering rows
* Date/time transformation
* Grouping data
* Aggregation with `sum`
* Sorting results
* Filtering aggregated results

## Author

**[Your Name]**

## License

This project is intended for educational purposes.
