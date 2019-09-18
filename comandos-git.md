#Comando de Git y Github

Una lista de comando usados por mi que ire actualizando día a día :trollface:

**Clonacion de repositorios**

~~~console
git clone https://github.com/HuAnPQ/comandos-linux.git
~~~

**Actualizar repositorio en local**

~~~console
cd Proyecto_a_actualizar
git pull
~~~

**Aperitivo(Add) Comida(Commit) Postre(Push)**

~~~console
git status
git add . --all
git commit -m "Comentarios de los cambios"
git push
~~~

**Etiquetado de versiones**

~~~console
git tag -a v1.0 -m "Version 1.0 - Primeros comandos"
git tag -n 
git push --tags
~~~

**Ramas Branch**

~~~console
git checkout -b modmarkdown
git add . --a
git commit -m "Cambiar extension de archivos"
git push -u origin modmarkdown
~~~



