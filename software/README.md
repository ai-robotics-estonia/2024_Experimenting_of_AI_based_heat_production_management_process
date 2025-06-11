# Industrial Automation Program for Mitsubishi FX3U Controller

This program is developed for an industrial controller based on the Mitsubishi FX3U platform, using **GX Works** (version 1.601L) as the development environment. The system features a modular logic structure, ensuring clarity, flexibility, and ease of maintenance for future development.

## External Data Integration

- **Electricity price data** from Nord Pool and **weather forecast data** (WethIN) are retrieved via the ModBus protocol from a weather station (Salve ID33).
- These inputs are essential for energy management and predictive logic.

## Input Configuration

- All controller inputs are described in detail within the `IO_CONF` module, providing a clear overview and easy configuration.

## Energy Management

- Modules related to energy usage and control logic are organized under the `Energy` module.
- This allows for monitoring and optimizing energy consumption based on forecasts and pricing data.

## Data Processing and Analysis

- Data sorting, copying, and maximum value detection are handled in the `SortData` module.
- This ensures all necessary values are available in the correct format and at the right time.

## Data Updating and Storage

- Data is automatically copied and updated daily at **15:00**, when new pricing and forecast information becomes available.
- The data is stored in two main structures:
  - `PRICE` – the electricity price table
  - `PtoGraph` – price data formatted for graphical representation (Price to Graph)