**Tabla de Contenidos**

- [Paso 1: Hacer fork al repositorio](#paso-1-hacer-fork-al-repositorio)
- [Paso 2: Clonar el repositorio](#paso-2-clonar-el-repositorio)
- [Paso 3: Crear conexión con el repositorio original](#paso-3-crear-conexión-con-el-repositorio-original)
- [Paso 4: Crear nuestra rama de trabajo](#paso-4-crear-nuestra-rama-de-trabajo)
- [Paso 5: Hacer los cambios necesarios](#paso-5-hacer-los-cambios-necesarios)
- [Paso 6: Guardar nuestros cambios y hacer commit](#paso-6-guardar-nuestros-cambios-y-hacer-commit)
- [Paso 7: Mezclamos las diferencias](#paso-7-mezclamos-las-diferencias)
- [Paso 8: Subimos la rama en la que hemos estado trabajando](#paso-8-subimos-la-rama-en-la-que-hemos-estado-trabajando)
- [Paso 9: Crear el pull request (PR)](#paso-9-crear-el-pull-request-pr)
- [Paso extra: Obtener nuevos cambios](#paso-extra-obtener-nuevos-cambios)


En esta guía veremos los conceptos necesarios para empezar a trabajar de manera colaborativa en un repositorio de Github a través de Git

El repositorio que estaremos usando para acompañar nuestra guía lo encuentras [aquí](https://github.com/catWhatWhat/PR-prueba). Este repositorio lo usaremos para mandar nuestros Pull Request.

### Paso 1: Hacer fork al repositorio

> Con "fork" nos referimos a que vamos a hacer una copia del repositorio
> de otra persona dentro de nuestra cuenta de Github

Cuando estemos dentro de la página del repositorio nos dirigiremos a la parte superior derecha y presionaremos el botón que dice `Fork`

![Foto del Fork](https://drive.google.com/file/d/16ZOoTsYDBZkaqVyq_LD70oPAZia4bYk_/view?usp=sharing)

Nos va salir una ventana similar a esta, donde podremos cambiar el nombre y la descripción al repositorio si es que así lo quisiéramos, en este caso lo dejamos igual y le damos a `Create fork`

![Foto de la ventana luego del fork]()

Luego de eso veremos que se ha copiado el repositorio a nuestra cuenta de github.

![Foto de la copia]()

### Paso 2: Clonar el repositorio

Una vez hecho el fork, vamos a proceder a clonar el repositorio que se ha copiado en nuestra cuenta. Este lo clonamos en algún lugar específico de nuestra computadora

> Nota: Cuando clonamos un repositorio, se crea una carpeta con el nombre del
> repositorio por lo que no hace falta crear una carpeta en específico para el proyecto

Para nuestro ejemplo vamos a clonar el repositorio en el escritorio

1. Abrimos Git Bash (o Windows Terminal si lo tienen instalado) y colocamos
	```bash
	cd Desktop
	# o
	cd Escritorio

	# Esto dependerá de como esté configurado tu sistema operativo owo
	```
2. Colocamos el comando
	```bash
	git clone <URL del repositorio>
	```
	Debemos asegurarnos de que el repositorio debe ser el que está en nuestra cuenta, en este caso el comando sería:
	```bash
	git clone https://github.com/ashel1806/PR-prueba.git
	```
	Esto va a crear una carpeta en nuestro Escritorio llamada `PR-prueba`
	
3.  Accedemos a nuestro repositorio clonado en nuestra computadora
	```bash
	cd PR-prueba
	```
	Y Listo!, ya tendriamos el repositorio clonado en nuestra computadora owo

### Paso 3: Crear conexión con el repositorio original

Cuando clonamos el repositorio de Github a nuestra computadora, de manera interna se crea una conexión hacia el repositorio original y se le asigna el nombre `origin`, si queremos comprobar esto podemos usar el comando:

```bash
git remote get-url origin
```

Aquí vemos que al ejecutar el comando nos muestra la url del repositorio de GitHub que se ha guardado en nuestra cuenta

Además de tener una conexión al repositorio de nuestra cuenta, es importante tener también una conexión hacia el repositorio original, a esta conexión se le asigna de manera convencional el nombre `upstream`

Para crear esta conexión debemos ejecutar el siguiente comando: 

```bash
git remote add <nombre de la conexión> <url del repositorio>
```
En nuestro caso sería: 

```bash
git remote add upstream https://github.com/catWhatWhat/PR-prueba
```

Vemos que no nos indica si la conexión se ha hecho correctamente, así que lo hacemos manualmente con el comando: 

```bash
git remote get-url upstream
```

En la imagen podemos ver que nos muestra la url del repositorio original 

### Paso 4: Crear nuestra rama de trabajo

Una vez dentro de nuestro repositorio local y luego de haber establecido la conexión al repositorio original, crearemos una nueva rama en la cual estaremos trabajando, con el nombre que deseemos, en este caso le llamaré `cambios`

Para crear una nueva rama en git usamos el comando:

```bash
git checkout -b <Nombre de la rama>
```

Para nuestro caso sería:

```bash
git checkout -b cambios
```

En la imagen vemos como es que se ha cambiado la palabra *main* por *cambios* (el nombre de la rama que acabamos de crear), esto es debido a que el comando `git checkout -b` además de crear  una nueva rama también nos posiciona en ella, moviéndonos de la rama principal (*main*) a la rama nueva que hemos creado (*cambios*)

### Paso 5: Hacer los cambios necesarios

En este paso vamos a estar realizando los cambios que deseemos hacer, podemos agregar los archivos y carpetas que sean necesarias.

Para nuestro ejemplo vamos a agregar un archivo de Javascript cuyo nombre será nuestro primer apellido y la inicial de nuestro nombre, por ejemplo, yo me llamo Ashel Joseph Vasquez Palomino, entonces mi archivo se llamará `vasquez-a.js`, y dentro de ese archivo vamos a escribir un `console.log` que imprima el mensaje 'El primer PR de' acompañado de nuestro nombre.

1. Dentro de nuestra rama vamos a colocar: 

	```bash
	code .
	```
	
	Esto nos abrirá la carpeta de nuestro repositorio dentro de Visual Studio Code

	Si observamos la parte inferior dentro de VS Code, notaremos que nos señala la rama en la que nos encontramos, esto es muy importante ya que en algunas ocasiones puede que estemos trabajando dentro de la rama principal (*main*) , lo cual es muy peligroso.

2. Creamos nuestro archivo
3. Colocamos el `console.log`
	> Si quieres ejecutar este archivo para que se imprima esto en la consola, debes tener
	> instalado [Node.js](https://nodejs.org/es/)

### Paso 6: Guardar nuestros cambios y hacer commit

Luego de realizar los cambios, o agregar el código que consideremos necesario, procederemos a guardar estos cambios

1. Le decimos a git que archivos han sido modificados y están listos para subirse

	Esto lo hacemos mediante el comando

	```bash
	# si son pocos los archivos a modificar
	git add <archivo-1> <archivo-2> ... <archivo-n>
	
	# si son varios archivos a modificar
	git add .
	
	# Con el "." indicamos que se van a subir todos los archivos 
	# de la carpeta que han sido agregados o modificados
	```

	En nuestro caso solo es 1 archivo, por lo que pondremos: 

	```bash
	git add vasquez-a.js
	```
	Para ver si ha sido agregado o no, podemos usar el comando `git status` que nos muestra el estado de los archivos que hemos modificado o agregado.
	
	Aquí nos muestra que hay un archivo que hemos agregado y que está listo para confirmar su subida al repositorio
	
2.  Confirmamos los archivos que se van a subir

	Esto lo hacemos mediante el comando:

	```bash
	git commit -m '<mensaje de confirmación>'
	```
	Dentro de `<mensaje de confirmación>`pondremos un mensaje descriptivo del cambio que acabamos de realizar. Este mensaje puede ser cualquiera que se les ocurra, siempre y cuando describa el cambio o modificación que hayamos realizado.
	
	Para seguir con nuestro ejemplo el mensaje será *"Nuevo PR de"* seguido de su nombre:

	```bash
	git commit -m 'Nuevo PR de Ashel Vasquez'
	```

	Este comando nos muestra cuantos archivos se han creado y/o modificado

### Paso 7: Mezclamos las diferencias

En este paso vamos a ejecutar un comando que mezcla cualquier diferencia (si es que las hay) entre el repositorio clonado en nuestra computadora con el repositorio que nosotros le indiquemos a travéz del nombre de su conexión, generalmente es el repositorio original, que en este caso tiene el nombre de `upstream`

Esto se realiza mediante el comando:

```bash
git pull <nombre de la conexion del repositorio> <rama a mezclar>
```

Para nuestro caso, vamos a mezclar las diferencias (si es que las hay) de la rama *main*, que es la rama principal del repositorio original

```bash
git pull upstream main
```
Si nos sale un mensaje de `Already up to date`, quiere decir que el repositorio original no tiene ninguna modificación

### Paso 8: Subimos la rama en la que hemos estado trabajando

Esto lo hacemos mediante el comando: 
```bash
git push <nombre de la conexion del repositorio> <rama a subir>
```

Nuestra rama se llama `cambios`, y debemos subir nuestra rama al repositorio que hemos creado nosotros, es decir a la conexión con nuestro repositorio que tiene como nombre `origin`: 

Entonces ponemos. 

```bash
git push origin cambios
```

En la imagen nos indica que debemos hacer un pull request (PR) dentro de nuestro repositorio

### Paso 9: Crear el pull request (PR)

Nos dirigimos a nuestro repositorio en GitHub y vemos que nos aparecerá un botón que dice `Compare & pull request`, el cual tenemos que presionar

Se nos abrirá una ventana similar a esta, en donde podremos modificar el título del PR que vamos a crear y agregar una pequeña descripción de los cambios que hemos agregado

Agregamos la descripción y le damos al botón `Create pull request`

Nos saldrá esta otra ventana en donde podemos ver varias opciones:
- Ver si nuetro PR tinene algun conflicto con el repositorio original
- Agregar comentarios al PR
- Cerrar el PR 

Ahora nos toca esperar a que el dueño del repositorio original acepte nuestro PR, nos deje una review, o que no lo acepte pero que nos dé una review de lo que debemos de cambiar

> Si no te aceptaron el PR y tienes cambios que realizar, no le des en Close pull request,
> esto hará que tengas que repetir algunos pasos de nuevo, por eso de preferencia déjalo
> así como está

Una vez que veamos que ha sido aceptado nuestro PR (el estado paso de *Open* a *Merged*), podemos proceder a eliminar la rama en la que hemos estado trabajando

Y ya estaría borrada nuestra rama del repositorio en GitHub :D

También la borraremos de nuestro repositorio local en nuestra computadora, para lo cual ejecutaremos los siguientes comandos en orden

```bash
# regresamos a la rama principal
git checkout main

# procedemos a eliminar la rama "cambios"
git branch -D cambios
```

### Paso extra: Obtener nuevos cambios

Si hay nuevos cambios dentro del repositorio original, tendremos que ejecutar:

```bash
git pull upstream main
```

De esta manera obtendremos los últimos cambios del repositorio original :D
