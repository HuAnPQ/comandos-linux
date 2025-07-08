# Averiguar el último login, fecha y DC de un usuario
Os dejo a continuación esta fantástica función que nos dice cual es el último timestamp del login de un usuario.

Para usarlo, copiar el código en ISE y llamar a la función.  Si queréis que sea permanente en vuestra navaja de utilidades, haced lo siguiente:

1) guardar el código con extensión .psm1

2) Crear una carpeta en "C:\Program Files\WindowsPowerShell\Modules" con el nombre Get-ADUserLastLogon y guardar el archivo ahí.


~~~powershell
function Get-ADUserLastLogon { 
# .SYNOPSIS
# Get-ADUserLastLogon obtiene la información del último login de un usuario en Active directory.
 
# .DESCRIPTION
# Cada controlador de dominio es consultado individualmente para calcular la fecha de último login.
 
# .PARAMETER
# UserLogonName
# Proveer la cuenta de usuario (samaccountname).
 
# .EXAMPLE
# Get-ADUserLastLogon -UserLogonName C.Melantuche
 
[CmdletBinding()]
param
(
[Parameter(Mandatory=$true)]
$UserLogonName
)
$resultlogon=@()
Import-Module ActiveDirectory
$ds=dsquery user -samid $UserLogonName
If ($ds) {
$getdc=(Get-ADDomainController -Filter *).Name
foreach ($dc in $getdc) {
Try {
$user=Get-ADUser $UserLogonName -Server $dc -Properties lastlogon -ErrorAction Stop
$resultlogon+=New-Object -TypeName PSObject -Property ([ordered]@{
'User' = $user.Name
'DC' = $dc
'LastLogon' = [datetime]::FromFileTime($user.'lastLogon') 
}) 
}
Catch {
''
Write-Warning "No reports from $($dc)!" 
} 
} 
$resultlogon | Where-Object {$_.lastlogon -NotLike '*1601*'} | Sort-Object LastLogon -Descending | Select-Object -First 1 | Format-Table -AutoSize 
If (($resultlogon | Where-Object {$_.lastlogon -NotLike '*1601*'}) -EQ $null)
{
''
Write-Warning "No hay datos para $($user.name). Posible razón: Nunca se ha logueado en el dominio."
}
}
else 
{throw 'Usuario inexistente. Por favor compruebe el usuario.'}
 
}
~~~
