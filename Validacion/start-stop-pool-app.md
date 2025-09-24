# Iniciar/Detener un Pool Aplication IIS

 

~~~powershell

param(
    [parameter(Mandatory=$true)]
    [string]$appPoolName,
    [parameter(Mandatory=$true)]
    [byte]$startPool
)
Write-Host("APPLICATION POOL: $appPoolName")
Write-Host("START APPLICATION POOL: $([bool]$startPool)")
$appPoolState = Get-WebAppPoolState -Name $appPoolName

if($appPoolState.Value -eq "Started" -and $startPool -eq 0){
    Stop-WebAppPool -Name $appPoolName
    Write-Host('THE APPLICATION POOL STOPPED SUCCESSFULLY.')
}
elseif($appPoolState.Value -eq "Stopped" -and $startPool -eq 1){
    Start-WebAppPool -Name $appPoolName
    Write-Host('THE APPLICATION POOL STARTED SUCCESSFULLY.')
}
else{
    if($startPool){
        Write-Host('THE APPLICATION POOL IS ALREADY STARTED.')
    }
    else{
        Write-Host('THE APPLICATION POOL IS ALREADY STOPPED.')
    }        
}
~~~
