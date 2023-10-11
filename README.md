# 79THGroupPrinters
```
$inf = "C:\printers\Konica-Minolta-C4050i\KOAXCA__.inf"
$drivername = "KONICA MINOLTA C4050iSeriesPS"
$printerName = "KONICA MINOLTA C4050i"
$printerPort = "10.10.10.12"
$printerPortName = "TCPPort:10.10.10.12"

#Create new printers folder on the C drive
New-Item -ItemType Directory -Path "C:\printers" -Force

#Download print drivers zip
curl -o C:\printers\Konica-Minolta-C4050i.zip "https://github.com/laws98/79THGroupPrinters/raw/main/Konica-Minolta-C4050i.zip"

#Unzip downloaded printer drivers
Expand-Archive C:\printers\Konica-Minolta-C4050i.zip -DestinationPath C:\printers -Force

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

#Delete newly created printers folder
Get-ChildItem -Path "C:\printers\*" | Remove-Item -Recurse -ErrorAction SilentlyContinue
```
