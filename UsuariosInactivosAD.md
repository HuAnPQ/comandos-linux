# Usuarios inactivos en AD

Script para encontrar todos los usuarios inactivos en base a 4 criterios para elegir 1, dos acciones disponibles a elegir 1 y generación de un reporte.


~~~powershell
Import-Module ActiveDirectory

# Selecciona los días de inactividad
$DaysInactive = 90
$InactiveDate = (Get-Date).Adddays(-($DaysInactive))

#-------------------------------
# Encontrar Usuarios inactivos
#-------------------------------
# A continuación 4 acciones para buscar usuarios inactivos. Selecciona la que sea más apropiada para ti o modfícala si lo necesitas.

# Obtén los usuarios que no se han logueado en los últimos XXXX días
$Users = Get-ADUser -Filter { LastLogonDate -lt $InactiveDate -and Enabled -eq $true } -Properties LastLogonDate | Select-Object @{ Name="Username"; Expression={$_.SamAccountName} }, Name, LastLogonDate, DistinguishedName

# Obtén los usuarios que no se han logueado en los últimos XXXX días y no son cuentas de servicios
$Users = Get-ADUser -Filter { LastLogonDate -lt $InactiveDate -and Enabled -eq $true -and SamAccountName -notlike "*svc*" } -Properties LastLogonDate | Select-Object @{ Name="Username"; Expression={$_.SamAccountName} }, Name, LastLogonDate, DistinguishedName

# Obtén los usuarios que no se han logueado nunca
$Users = Get-ADUser -Filter { LastLogonDate -notlike "*" -and Enabled -eq $true } -Properties LastLogonDate | Select-Object @{ Name="Username"; Expression={$_.SamAccountName} }, Name, LastLogonDate, DistinguishedName

# Automatizado incluyendo los que no se hanlogueado
$Users = Search-ADAccount -AccountInactive -DateTime $InactiveDate -UsersOnly | Select-Object @{ Name="Username"; Expression={$_.SamAccountName} }, Name, LastLogonDate, DistinguishedName

#-------------------------------
# Creación de reporte
#-------------------------------
# Exportarlo a CSV (Debéis tener creado el directorio c:\TEMP)
$Users | Export-Csv C:\Temp\InactiveUsers.csv -NoTypeInformation

#-------------------------------
# Administración de usuarios inactivos
#-------------------------------
# A continuación 2 acciones para buscar usuarios inactivos. Selecciona la que sea más apropiada para ti o modfícala si lo necesitas.
# Deshabilitar los usuarios inactivos
ForEach ($Item in $Users){
  $DistName = $Item.DistinguishedName
  Disable-ADAccount -Identity $DistName
  Get-ADUser -Filter { DistinguishedName -eq $DistName } | Select-Object @{ Name="Username"; Expression={$_.SamAccountName} }, Name, Enabled
}

# Borrado de usuarios inactivos
ForEach ($Item in $Users){
  Remove-ADUser -Identity $Item.DistinguishedName -Confirm:$false
  Write-Output "$($Item.Username) - Deleted"
}
~~~
