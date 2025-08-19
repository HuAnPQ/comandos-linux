## Abrir remote como administrador

```cmd
mstsc /admin
```
 

## Registrar entradas de EventViewer
```cmd
[System.Diagnostics.EventLog]::CreateEventSource("CoreAdministracionClientes","CoreAdministracionClientes")
```

 

## Validar version del .Net Framework

C:\Windows\Microsoft.NET\Framework\v4.0.30319>MSBuild.exe -version

 

## Validar dominio

```cmd
nslookup
```
 

## Lista de Sdk y runtimes

```cmd
dotnet --list-sdks

dotnet --list-runtimes
 ```

## Refrescar los dns

```cmd
ipconfig /flushdns
 ```
Successfully flushed the DNS Resolver Cache.

 

## Eliminar logs

```cmd
del *.log /F /S /Q
```
 

## Listar directorio ordenado e incluir subcarpetas

```cmd
dir /O:N /S
```
 

## Desencriptar appsetting de sitio IIS
```cmd
cd "c:\Windows\Microsoft.NET\Framework\v4.0.30319"

aspnet_regiis.exe -pdf "appSettings"  "F:\config"

aspnet_regiis.exe -pdf "connectionStrings"  "F:\config"
```
