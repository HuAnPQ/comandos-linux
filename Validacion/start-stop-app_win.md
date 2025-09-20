# Detener/Iniciar un aplicativo

 

~~~powershell

    Write-Host "Detener los procesos Prometeus"

    Stop-Process -Name "Prometeus" -Force -erroraction 'silentlycontinue' -PassThru

 

    Write-Host "Iniciando Prometeus..."

    $prometeusProcess = Start-Process -FilePath $pathPrometeus -WorkingDirectory $pathDirPrometeus -NoNewWindow -PassThru

    $prometeusProcess

~~~

