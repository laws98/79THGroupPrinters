# 79THGroupPrinters
```
$inf = "C:\printers\KOAZ8A__.INF"
$drivername = "KONICA MINOLTA C360SeriesPS"
$printerName = "KONICA MINOLTA C220"
$printerPort = "10.10.10.11"
$printerPortName = "TCPPort:10.10.10.11"

New-Item -ItemType Directory -Path "C:\printers" -Force

curl -o C:\printers\KOAZ8A__.INF "https://raw.githubusercontent.com/laws98/79THGroupPrinters/main/KOAZ8A__.INF"

# Install the driver
PNPUtil.exe /add-driver $inf /install

# restart print service
Restart-Service -Name 'Spooler'

# Add driver to the list of available printers
Add-PrinterDriver -Name $DriverName -Verbose

# Add a network printer port
Add-PrinterPort -Name $printerPortName -PrinterHostAddress $printerPort -ErrorAction SilentlyContinue

# restart print service
Restart-Service -Name 'Spooler'

#Add the printer
Add-Printer -DriverName $DriverName -Name $printerName -PortName $printerPortName -Verbose
```
