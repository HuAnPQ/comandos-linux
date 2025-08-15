
## Comando powershell validar conexion

Test-NetConnection notify.entrust.com -Port 443 -InformationLevel "Detailed"

 
## Log en Componentes .Net

```cshard
System.Diagnostics.EventLog.WriteEntry("Aplication",

                    "ex.Message" + ex.Message + "ex.StackTrace" + ex.StackTrace + "ex.InnerException" + ex.InnerException,

                    System.Diagnostics.EventLogEntryType.Information, 2006, 1);
```
 

## Registrar entradas de EventViewer

```Powershell

Remove-EventLog -Source "WebBFF.ProdunetAdmin.Identidad"

New-EventLog -LogName WebBFF.Produnet -Source WebBFF.ProdunetAdmin.Identidad
```
 
## Reglas de Nlog
```xml
<logger name="*" minlevel="Debug" maxlevel="Error" writeTo="jsonFile"/>
```
