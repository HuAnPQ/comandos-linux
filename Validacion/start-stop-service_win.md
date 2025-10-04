# Iniciar/Detener servicios windows

 

~~~powershell

Param(
  [Parameter(Mandatory = $true)]
  [bool] $EstaIniciar,
  [Parameter(Mandatory = $true)]
  [String] $PathServicios,
  [Parameter(Mandatory = $false)]
  [int] $ServiciosNOIniciadosNecesarios = 5
)

 

#region Imprimir las variables de entrada
Write-Host "Es Stopped(False) o Running(True):" $EstaIniciar
Write-Host "Direccion lista de servicios Windows:" $PathServicios
Write-Host "Numero de servicios no Iniciados(Aplica para levantar servicios):" $ServiciosNOIniciadosNecesarios
Write-Host ([string]::Empty)
#endregion

$estado = "Stopped"
$ServiciosNOIniciados = 0

try {
    if( $EstaIniciar ){
        $estado ="Running"
        Write-Host "--- Iniciar los servicios"
        ForEach ($servicio in Get-Content $PathServicios) {
            if ( Get-Service | Where-Object {$_.Name -eq $servicio -and $_.Status -ne $estado -and $_.StartType -ne "Disabled" } ){
                Write-Host "Iniciando el servicio -> " +  $servicio
                Start-Service -Name $servicio -ErrorAction SilentlyContinue
            }
        }
    }
    else {
        Write-Host "--- Detener los servicios"
        ForEach ($servicio in Get-Content $PathServicios) {
            if ( Get-Service | Where-Object {$_.Name -eq $servicio -and $_.Status -ne $estado -and $_.StartType -ne "Disabled" } ){
                Write-Host "Deteniendo el servicio -> " +  $servicio
                Stop-Service -Name $servicio -Force -ErrorAction SilentlyContinue
            }
        }
    }
    # Validar si que servicios No subieron
    if( $EstaIniciar ){
        Write-Host "--- Validar que servicios NO subieron"
        ForEach ($servicio in Get-Content $PathServicios) {
            if ( Get-Service | Where-Object {$_.Name -eq $servicio -and $_.Status -ne $estado } ){
                Write-Host "Servicio NO Iniciado -> " +  $servicio
                $ServiciosNOIniciados ++
            }
        }
        Write-Host "---- Lista de servicio con Logon corptest\salgadom"
        Get-WmiObject win32_service | Where-Object {$_.StartName -eq "corptest\salgadom" } | Sort-Object -Property StartName | Select Name, StartMode, State
    }
    exit 0
}
catch [Exception] {
    Write-Host ([string]::Format("ERROR: {0}", $_.Exception.Message)) -ForegroundColor Red
    exit 1
}

Write-Host 'Fin del Proceso'

~~~

