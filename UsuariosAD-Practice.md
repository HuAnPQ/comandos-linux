
Practica de Crear, listar usuarios de AD desde Powershell

~~~powershell
#Comandos a aprender

#New-ADUser = Crear usuarios

#Remove-ADUser = Borrar usuarios

#Get-ADUser = Listar/verificar usuario

#Set-ADUser = Modificar usuario



#Crear un usuario

New-ADUser Sole



#Borrar un usuario

Remove-ADUser Sole



#Crear un usuario con propiedades

New-ADUser -Name Sole -City Madrid -Company NoSoloHacking -Department Marketing -Description "Buena Gente" -DisplayName "Sole García" -EmailAddress sole@nosolohacking.info -Manager Carlos -Office "Edificio 1" -OfficePhone "+34 916524578" -Organization NoSoloHacking



#Mostrar un usuario

Get-ADUser -Identity sole



#Mostrar un usuario con todas alguna de propiedades

Get-ADUser -Identity sole -Properties description, city, department



#Mostrar un usuario con todas sus propiedades

Get-ADUser -Identity sole -Properties *



#Crear un usuario con propiedades y contrasena #ERROR

New-ADUser -Name Sole -AccountPassword 123456Aa -City Madrid -Company NoSoloHacking -Department Marketing -Description "Buena Gente" -DisplayName "Sole García" -EmailAddress sole@nosolohacking.info -Manager Carlos -Office "Edificio 1" -OfficePhone "+34 916524578" -Organization NoSoloHacking



#Crear usuario sin best practices

Remove-ADUser sole

New-ADUser sole -AccountPassword $(convertto-securestring "123456Aa" -AsPlainText -force)

Get-ADUser Sole

get-history



#Crear usuario con best practices



#Crear una variable para el usuario Password

$password = Read-host "Escribe una contrasena" -AsSecureString



#crear usuario con la nueva password de $password

Remove-ADUser -Identity sole

Get-ADUser sole

New-ADUser -Name Sole -City Madrid -Company NoSoloHacking -Department Marketing -Description "Buena Gente" -DisplayName "Sole García" -EmailAddress sole@nosolohacking.info -Manager Carlos -Office "Edificio 1" -OfficePhone "+34 916524578" -Organization NoSoloHacking -AccountPassword $password

Get-ADUser sole

Enable-ADAccount -Identity sole



#Modificar un usuario

Set-ADUser -Identity sole -Description "Smart"

Set-ADUser -Identity sole -Description "Smart" -city "London"
~~~
