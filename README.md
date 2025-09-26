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

### Change WebAPI port
You can change the WebAPI port by adding it on the the end of a config that already has COM and BaudRate set. Provide anything other then 8000 and it will retain the setting.
```
CostPerKW|TotalKWUsed|COM1|9600|WebAPI
```

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

* Adding [sqlite3.dll](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/sqlite3.dll) and [System.Data.SQLite.dll](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/System.Data.SQLite.dll) to the same folder as RackPowerUPSConsole.exe will trigger the application to dump each sample from the UPS to ups_logs.db. This can be used to view graphs of data over time. It will consume about 720kb per hour.<br>
![Screenshot](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/SQLiteGraph.png?raw=true)

---

## 📊 Grafana

* You can view the ups_logs.db (SQLite database) with Grafana. There is a dashboard template here [Grafana-Dashboard-RackPower.json](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/Grafana-Dashboard-RackPower.json)<br>
![Screenshot](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/Grafana12-screenshot.png?raw=true)

---

## 📊 Web API

* Adding [index.html](https://raw.githubusercontent.com/bmgjet/RackPowerUPS-ConsoleClient/refs/heads/main/index.html) to the same folder as RackPowerUPSConsole.exe will trigger the application to open a WebAPI port at 8000 unless set in the config. [How To Set Port](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/README.md#change-webapi-port)<br><br>Examples and information with in the example index.html here. You can make the file empty or put anything you want in it and it will still function.<br>You can access the SQLite db file directly with the web api enabled and the SQLite.dll installed. <br>Example: http://localhost:8000/ups_logs.db
<br>![Screenshot](https://github.com/bmgjet/RackPowerUPS-ConsoleClient/blob/main/webapi-screenshot.png?raw=true)
---

## 🛠️ Notes

* Make sure UPS serial port is configured correctly
* Use the COM port that appears in Windows Device Manager
* Only tested with Power Rack 3000W UPS, But should work with 1000W, 2000W Models and 6000W and 10000W with reduced information.
* Requires .NET Framework 4.7+

## Library File Source Code
https://github.com/bmgjet/RackPowerUPS-Library

## Rack Power Website
https://rackpower.co.nz/product-category/ups/tower/
