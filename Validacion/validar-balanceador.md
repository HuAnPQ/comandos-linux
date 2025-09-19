# Subir o bajar el balanceador NLB

~~~powershell
param(
    [parameter(Mandatory=$true)]
    [bool]$startNode
)
Write-Host("START(True) O STOP(False): $startNode")

if($startNode){
    Start-NlbClusterNode -HostName $env:COMPUTERNAME
    Write-Host('LEVANTANDO EL NODO EN LA NLB. ' + $env:COMPUTERNAME)
}
else{
    Stop-NlbClusterNode -HostName $env:COMPUTERNAME
    Write-Host('BAJANDO EL NODO EN LA NLB. ' + $env:COMPUTERNAME)
}
Get-NlbClusterNode
Get-Date -Format "dddd MM/dd/yyyy HH:mm"
~~~

 

