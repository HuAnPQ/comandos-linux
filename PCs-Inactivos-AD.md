# PCs Inactivos en AD

Script para encontrar todos los PCv inactivos en base a 3 criterios para elegir 1, dos acciones disponibles a elegir 1 y generación de un reporte.

~~~powershel
Import-Module ActiveDirectory

# Selecciona los días de inactividad
$DaysInactive = 90
$InactiveDate = (Get-Date).Adddays(-($DaysInactive))

#-------------------------------
# Encontrar objetos de tipo PCs inactivos
#-A continuación 3 acciones para buscar PCs inactivos. Selecciona la que sea más apropiada para ti o modfícala si lo necesitas.

# Obtén los PCs que no se han logueado en los últimos XXXX días
$Computers = Get-ADComputer -Filter { LastLogonDate -lt $InactiveDate -and Enabled -eq $true } -Properties LastLogonDate | Select-Object Name, LastLogonDate, DistinguishedName

# Obtén los PCs que no se han logueado nunca
$Computers = Get-ADComputer -Filter { LastLogonDate -notlike "*" -and Enabled -eq $true } -Properties LastLogonDate | Select-Object Name, LastLogonDate, DistinguishedName

# Automatizado incluyendo los que no se hanlogueado
$Computers = Search-ADAccount -AccountInactive -DateTime $InactiveDate -ComputersOnly | Select-Object Name, LastLogonDate, Enabled, DistinguishedName

#-------------------------------
# Creación de reporte
#-------------------------------
# Exportarlo a CSV (Debéis tener creado el directorio c:\TEMP)
$Computers | Export-Csv C:\Temp\InactiveComputers.csv -NoTypeInformation
#-------------------------------
# Administración de usuarios inactivos
#-------------------------------
# A continuación 2 acciones para buscar usuarios inactivos. Selecciona la que sea más apropiada para ti o modfícala si lo necesitas.

# Deshabilitar los PCs inactivos
ForEach ($Item in $Computers){
  $DistName = $Item.DistinguishedName
  Set-ADComputer -Identity $DistName -Enabled $false
  Get-ADComputer -Filter { DistinguishedName -eq $DistName } | Select-Object Name, Enabled
}

# Borrado de PCs inactivos
ForEach ($Item in $Computers){
  Remove-ADComputer -Identity $Item.DistinguishedName -Confirm:$false
  Write-Output "$($Item.Name) - Deleted"
}
~~~
