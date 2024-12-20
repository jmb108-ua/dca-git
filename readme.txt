JUAN MARTINEZ BLASCO

Repositorio publico Github:
https://github.com/jmb108-ua/dca-git.git

Hemos comenzado haciendo algunas configuraciones globales que podemos ver con:

  $ git config --global --list

Luego hemos creado varias ramas locales y despues subidas al remote en github.

Mas tarde provocabamos un fallo añadiendo diferentes commits y marcando algunos como erroneos 
y otros como buenos con las herramientas de git bisect:
  $ git bisect start
  $ git bisect bad
  $ git bisect good
  $ git bisect reset

Con este ultimo comando reseteamos los commits que no eran correctos.

Por ultimo, implementamos una condicion con un hook pre-commit para que no se puedan subir
commits si este no se cumple.

A continuación, copio la secuencia de como probe el hook y al principio daba error pero luego al cumplir la condicion si me dejaba hacer commits:

  $ git status
   	En la rama main
	Tu rama está adelantada a 'origin/main' por 3 commits.
  	(usa "git push" para publicar tus commits locales)

	nada para hacer commit, el árbol de trabajo está limpio

  $ git add .
  $ git commit -m "Prueba del hook."

	Ejecutando el hook pre-commit
	Error: archivo.txt no contiene 'FIXED'.

  $ git status

	En la rama main
	Tu rama está adelantada a 'origin/main' por 3 commits.
	(usa "git push" para publicar tus commits locales)

	Cambios no rastreados para el commit:
	(usa "git add <archivo>..." para actualizar lo que será confirmado)
	(usa "git restore <archivo>..." para descartar los cambios en el directorio de trabajo)
	modificados:     archivo.txt

	sin cambios agregados al commit (usa "git add" y/o "git commit -a")

  $ git add .
  $ git commit -m "Codigo arreglado para que no salte error del hook. (el archivo contiene FIXED)"
	Ejecutando el hook pre-commit
	[main 39317d4] Codigo arreglado para que no salte error del hook. (el archivo contiene FIXED)
	1 file changed, 3 insertions(+)


Como vemos en este ultimo commit ya nos deja commitear al tener FIXED en nuestro archivo.txt
