# RackPower UPS Console Client

Software to connect to **Power Rack 3000W UPS** over serial (RS-232/USB).<br>
**Download:** [RackPowerUPSConsole.exe](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/RackPowerUPSConsole.exe) and [RackPower.dll](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/RackPower.dll)


![Screenshot](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/PowerRackConsole-Screenshot.png?raw=true)

---

## ⚙️ Requirements

* DB9 Serial to USB adapter
* UPS configured via user manual for serial communication

### Serial Setup on UPS

1. Hold `Function` + `ON/OFF` for 3 seconds
2. Navigate to menu `232` using the `FUNC` button
3. Press `ON/OFF` to select
4. Set:

   * Baud rate: `96`
   * COMID: `1`
   * Protocol: `1cc`
5. Final screen should look like:

   ![Example Screen](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/ExampleScreen.png?raw=true)

### PC Setup

* Plug Serial to USB adapter into PC
* Install drivers and note the COM port in Device Manager

---

## 🚀 Getting Started

1. Run the console application
2. Connect using the COM port and `9600` baud rate
3. On first startup, `config.txt` will be created: It contains the information to calculate $ power used, Config layout:

```
CostPerKW|TotalKWUsed
```

### Optional Auto Connect

Add `|Com|BaudRate` to the end of the file:

```
CostPerKW|TotalKWUsed|COM1|9600
```

The application will auto-connect using these settings.

---

## 📊 Features

* Poll UPS status every second
* Display UPS information including:

  * Voltages, currents, frequencies
  * Battery voltage, current, capacity, temperature, remaining time
  * Load, watts, VA
  * Charger current, inverter voltage, IGBT temps
  * Total energy usage and cost
* Save persistent configuration (cost per kWh, total kWh, COM port, baud rate)

---

## 📊 SQLite

* Adding [sqlite3.dll](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/sqlite3.dll) to the same folder as RackPowerUPSConsole.exe will trigger the application to dump each sample from the UPS to ups_logs.db. This can be used to view graphs of data over time. It will consume about 600kb per hour.<br>
![Screenshot](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/SQLiteGraph.png?raw=true)

---

## 🛠️ Notes

* Make sure UPS serial port is configured correctly
* Use the COM port that appears in Windows Device Manager
* Only tested with Power Rack 3000W UPS, But should work with 1000W, 2000W, 6000W and 10,000W Models
* Requires .NET Framework 4.7+

## Library File Source Code
https://github.com/bmgjet/RackPowerUPS-Library

## Rack Power Website
https://rackpower.co.nz/product-category/ups/tower/
