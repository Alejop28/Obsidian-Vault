**Usos de Git**
-Historial
-Almacenar código
-Trabajar en equipo
-Saber cuando se introdujo el error en un software

**Comandos básicos**
`git --version`
`git config --global` (Para que la config que agreguemos sea de manera global)
`core.editor` (Asigna editor de codigo por defecto)
`--wait` (Para que la terminal se quede esperando hasta que cerremos el editor de texto)

Si quiero ver  mi archivo de configuración global, pongo lo siguiente:
`git config --global -e`  (Si todo está bien, debería verse mi archivo en vs code)
![[Pasted image 20240817213621.png]]

Vamos a ver una configuración importante: `core.autocrlf` Se usa para tratar los saltos de línea en caso de que estemos trabajando varias personas con diferentes SO´s
Si estoy en windows: `git config --global core.autocrlf true`
Si estoy en Mac/Linux: `git config --global core.autocrlf input`
`git config -h` : Me da listado de todas las configuraciones
**Comandos**
`ls` : Permite listar todos los archivos de un determinado directorio
`pwd` : Para saber en qué carpeta o directorio estoy
`cd <carpeta a la que me quiero mover>` : Moverme a una carpeta
`cd ..` :Si me quiero salir de la carpeta o directorio (Son lo mismo, windows carpetas, mac/linux directorios)
`mkdir <Nombre>` :Para crear nueva carpeta
`git init` :Para inicializar una carpeta como si fuese un proyecto a gestionar con Git

![[Pasted image 20240818023312.png]]
el .git significa que la carpeta está oculta
para mostrarla se usa `ls -a`
Para acceder a esta, ponemos `cd .git`

![[Pasted image 20240818023745.png]]
Esto es un **Detalle de implementación** aquí es donde se van a almacenar las versiones de nuestro código, absolutamente todo

Cuando trabajemos en nuestro computador, los cambios no se suben de inmediato al repositorio, para esto se llama al `git add`, este comando pasa los archivos a una etapa llamada `stage`, es una etapa intermedia para indicar cuales son los cambios efectuados para pasar al repositorio, no pasan todos, solo los que seleccionemos.
Si ya tengo todo listo para subir al repositorio llamamos al `git commit` y se puede eliminar lo que está en stage, luego viene otra etapa y es que los cambios que hayamos comprometido los podemos subir a la nube mediante `git push`.
Si quiero eliminar un archivo que ya envié al repositorio debo hacer el mismo proceso indicando que el archivo ha sido eliminado, esto para llevar registro de todo lo que se hace
![[Pasted image 20240818204614.png]]

`Code .` : Se usa para abrir en el editor la carpeta en la que me encuentro 

Tras haber realizado cambios desde el editor de codigo, vuelvo a git bash y veo el estado con
`git status` debería aparecer el No commits yet, ahora necesitamos seleccionar los cambios realizados con `git add` el último argumento de la función puede ser de varias formas, ya sea por:
- Nombre del archivo (Archivo1.txt)
- Extension: .txt   Esto lo que hará será agregar todos los archivos con esta extensión
-  `git add .` : El punto lo que hará será agregar todos los archivos que se tengan en rojo cuando llame al `git status` esto es una **mala práctica** y es porque quizá se nos olvide que estábamos editando otra cosa, que hayan imágenes o .exe que no queramos subir, esto solo haría innecesariamente más grande el repositorio.
![[Pasted image 20240818205908.png]]
Lo que está en verde son los archivos listos para ser comprometidos
Si quiero agregar varios archivos por nombre sería con el  `git add` y el nombre de los archivos separados por  un espacio

Si en la etapa de stage yo hago cambios a los archivos que subí con `git add` puedo ver nuevamente el `git satus` y me dirá que los cambios no están en etapa de stage, para subir los cambios necesito agregar de nuevo el archivo con el `git add`
![[Pasted image 20240818210658.png]]

Ojo, lo que estoy pasando a stage aquí, no son los archivos mismos sino los cambios que he realizado
Para comprometer o hacer commit a mi trabajo, hay 2 formas principales:
La primera y recomendada es mediante `git commit -m "texto con sentido aquí"`
![[Pasted image 20240818211208.png]]
Si tras haber modificado nuevamente un archivo en lugar de `git commit -m` pongo `git commit`
me abrirá el editor de texto para que yo documente el cambio que realicé, es importante guardar y cerrar la pestaña en el vs para poder continuar en el gut bash.

Ahora para eliminar archivos dentro del repositorio usamos `rm+nombre del archivo`
Al eliminar o hacer un cambio y le damos al `git status` los archivos que aparecen en rojo es porque no están en etapa stage
![[Pasted image 20240818213014.png]]
Si me quiero saltar el `git add`, pongo solamente `git rm (nombre del archivo)`
pasará directamente a stage, listo para hacerle commit
Si por alguna razón quiero sacar un cambio que pasé a la  etapa de stage, para eso se usa el comando `git restore --staged (Nombre del archivo)`
Para recuperar el archivo uso `git restore (Nombre del archivo)`
`mv` :Comando para poder mover archivos y se le indica el origen o archivo, seguido del destino o nuevo nombre
`mv archivo1.txt archivo.txt`
Luego se tienen que pasar a etapa de stage, ya que se hicieron 2 cambios, se borró y renombró
![[Pasted image 20240818214656.png]]
Para renombrar y agregar inmediatamente a stage los cambios el comando es:
`git mv`

**Como ignorar archivos?**
Para que estos no sean incluidos en repositorios de git, habrá ocasiones en las que no quiera montar ciertos archivos como al trabajar con variables de entorno, por ejemplo, si estoy trabajando con una base de datos y esa base de datos la tengo instalada en local y es para estar trabajando con ambiente de desarrollo, en ese caso, usuarios, contraseñas o cualquier otro tipo de acceso va a ser diferente al de producción, ya que quiero que esto esté en mi maquina pero que no se suba por error al repositorio ya que no quiero que otras personas conozcan mis contraseñas y además quiero que esto sea configurable de forma que cuando se despliegue a producción solo una persona tenga acceso a esas variables de entorno las cuales servirán para configurar la api y que se conecte con la base de datos de producción.

`.env`: Es un nombre estándar para variables de entorno
Para evitar hacer commit a un archivo que no queremos, en el vs creamos otro archivo llamado `.gitignore` y  ahí puedo escribir los archivos que quiero ignorar, también funciona con carpetas 

Un tip útil al momento de ver el estado en git, es una forma más elegante del `git status`, se puede utilizar cuando ya se tiene experiencia usando git, sería: `git status -s`
Si aparece una M en rojo quiere decir que el archivo ha sido modificado 
Si aparece ?? en rojo quiere decir que el archivo no ha sido agregado para hacer seguimiento 
Tras usar git add en el archivo nuevo, al poner el git status -s aparecerá una A en verde, quiere decir que el archivo ha sido agregado
![[Pasted image 20240819202131.png]]

**Como ver los cambios de una manera más visual?**
Tras realizar modificaciones, puedo usar el comando, `git diff` y me mostrará qué cambios se realizaron.
![[Pasted image 20240819202606.png]]
Por qué muestra que elimina "chanchito feliz" y después la vuelve a agregar?
Lo que pasa es que antes esta línea estaba sola y no existía un salto de línea, lo que hizo el editor fue poner el comando de salto de línea al final y por eso eliminó y volvió a poner la línea

Los @@ indican la versión
El comando git diff --staged muestra los cambios que se encuentran en etapa de stage

**Historial**
Para ver el historial de todo el repositorio se usa `git log` ahí veremos correo y nombre de la persona que realizo cierto commit, para un historial más agradable `git log --oneline`
Esto también va a mostrar el mensaje que se ponga dentro del commit, por esto es importante que el comentario que dejemos al hacer el commit tenga sentido.

**Hasta ahora...**

Hemos venido trabajando de manera lineal, colocando cambios respecto a algo que está en el pasado, pero qué ocurre cuando hay varios programadores trabajando en u mismo proyecto, ahí es donde entran bifurcaciones o ramas, en git son branches. Para salir de la rama principal y trabajar en nuestro código o corregir el error y recién ahí intentar devolvernos a la rama principal.

Antes de crear una rama primero debemos verificar en qué rama nos encontramos para eso 
`git branch` para crear una rama debemos escribir `git checkout -b (Nombre de la rama)`
El comando `cat (Nombre del archivo)` esto mostrará el contenido de nuestro archivo
Los cambios que se realizan en otra rama, no se reflejan en la principal

![[Pasted image 20240819213501.png]]
Para traer los cambios de otra rama a la principal usamos `git merge (Nombre de la rama que quiero traer)` siempre estando seguro de estar en la rama a la que se quieren traer los cambios

![[Pasted image 20240819215055.png]]
Así cada programador implementa su código en una rama sin estar todos trabajando en la rama principal

Cómo subir el repositorio a la nube?
Usamos el `git remote` que usamos para indicar si tenemos un servidor remoto en el cual vamos a subir nuestros cambios, en este caso 
`git remote add origin https://github.com/Alejop28/miweb.git`
con el add origin estamos indicando de donde vamos a obtener nuestro código y a donde subir los cambios que se realicen, seguido se monta la url de donde se encuentra el código

`git push` es el comando para que podamos subir los cambios respecto a la rama en la que estemos trabajando pero en el repositorio no está creada la rama, para esto se usa el -u  y le indicamos en origen(donde queremos que sea creada) que queremos que la rama se llame main`git push -u origin main`

Ya para continuar haciendo cambios sobre estos archivos se hace el mismo procedimiento; se realizan cambios en el editor de código, se hace el add, commit y por último se pone la línea 
`git push`
En el caso que se cree una nueva rama y aún no le quiera hacer un merge con master pero aún así quiero que esté en el repositorio lo que hago es cambiarme a la rama y cuando todo esté listo escribo `git push -u origin (Nombre de la rama)` y esto creará la rama en el repositorio