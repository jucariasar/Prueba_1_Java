# Notas sobre Git

## A tener en cuenta
+ Git es un VSC[^1] muy utilizado.
+ Existen tres zonas para un archivo: el **directorio de trabajo**, el **índice** y el **repositorio**.
+ El comando **"git status"** permite mostar el estado de los arhivos del repositorio Git[^2].
+ La zona **directorio de trabajo** es el directorio del sistema de archivos donde trbaja el desarrollador.
+ Git puede conocer[^3] los archivos que se encuentran en el **directorio de trabajo**, si han sido añadidos al menos una vez en Git.
+ El **índice** es en cierto modo una zona de espera de commit independiente del directorio de trabajo.
+ Un archivo que se encuentre solo en el **directorio de trabajo**, y que no haya sido añadido nunca al **índice**, es un archivo totalmente desconocido para Git; este tipo de archivo se conoce también como **archivo no seguido (untracked file)**.
+ Para añadir un archivo expecífico al **índice**, si este se encuentra en una carpeta, hay que especificar la ruta a partir de la carpeta de Git; por ejemplo C++/archivo.cpp.
+ Un archivo que se ha añadido al **índice** no se considera un archivo no seguido.
+ El hecho de que Git haya asignado un identificador (hash) al contenido del archivo significa que **Git ha integrado adecuadamente el archivo a su sistema**.
+ En la zona **repositorio**, Git **versiona al archivo** que contiene al menos una versión. El archivo es seguido **(tracked)** por Git y será considerado como modificado si el **hash del archivo en el directorio de trabajo** es diferente del **hash registrado en el repositorio**.
+ Incluso un cambio como un espacio en blanco o una linea en blanco en un archivo previamente seguido, es suficiente para que Git considere dicho archivo como modificado.
+ Para que un archivo pase del **índice** al **repositorio**, se requiere efectuar el **commit**.
+ El **commit** es el concepto fundamental de Git.
+ Al ejecutar el comando **"commit"**, se creará un paquete virtual que contiene un conjunto de modificaciones con el título definido por el argumento **"-m"**.
+ La zona repositorio contiene todos los commits del proyecto. Esto significa que **todo el historico del proyecto** se ubica en el repositorio.
+ Cuando se ejecuta el commit, Git recupera el archivo situado en el índice y lo añade al repositorio. Luego, Git elimina el archivo del índice; dado que esta es una **zona de espera**, ya no existe razón para que se encuentre aquí el archivo.
+ Si el proyecto tiene un solo archivo, no confundir el **hash del archivo** con el **hash del commit** que se realice; son **hash totalmente diferentes**.
+ A partir de que se añade con el comando add un archivo por primera vez al **"índice"** y posteriormente con el comando **"commit"** al repositorio, este archivo no se cosidera como un archivo no seguido, pero esto no significa que si posteriormente se modifica no haya que añadirlo de nuevo al **"índice"**, siempre que se modifique un archivo añadido anteriormente al **"índice"** y al **"repositorio"**, se debe añadir de nuevo al **"índice"** con el comando **"add"** para un próximo **"commit"**.
+ El comando **git ls-files --stage**, muestra todos los archivos seguidos con su identificador **hash**, se muestra tanto los archivos seguidos que estan en el **índice** como los que estan en el **directorio de trabajo**.
+ Una vez que un archivo se ha agregado al índice y posteriormente al repositorio, este ya no se mostrara como un archivo no seguido cuando se digite el comando **git status**.
+ En realidad para comprobar si hay cambios, Git compara el directorio de trabajo con **HEAD**[^4].



[^1]: Sistema de gestión de versiones (Source Content Management), también es utilizada la sigla VCS (Versión Control System)
[^2]: En este punto cuando se refieren al "repositorio Git", se hace referencia a la carpeta del proyecto, y no a la zona repositorio.
[^3]: Con "conocer" quiero decir que puede detectar modificaciones que se realicen posteriormente en un archivo.
[^4]: HEAD es una referencia (es decir, un acceso directo de Git) que apunta hacia el commit más reciente en la rama actual. De forma mas simple, HEAD es la versión actual guardada en el repositorio.

---

## Comandos

### Aspectos Generales

+ Para mostrar la ayuda general:
	git --help

+ Para obtener una ayuda mas completa sobre un comando específico de Git:
	git *comando_git* --help


### Tipos de comandos Git

Git propone una serie de comandos que se dividen en dos categorias:

+ Los **comandos de porcelana** (*porcelain command* en inglés).
+ Los **comandos de fontaneria** (*plumbing commands* en inglés)

Los **comandos de porcelana**: estos son los comandos de alto nivel. Son los comandos que se utilizan a diario y para los que Git propone una serie de controles. Por ejemplo, **git commit** y **git add** son comandos de porcelana.

Los **comandos de fontanería**: estos son los comandos de bajo nivel, es decir, que manipulan directamente la información que constituye el núcleo de Git. Estos comandos pueden ser destructivos para el repositorio y suelen ser aplicados por usuarios que dominan Git.


+ **Ayuda de los comandos de fontanería**

Por defecto, el comando **git help** no remite a los comandos de fontanería. Para ver todos los comandos Git (comandos de porcelana y fontanería), hay que utilizar el parámetro **-a** (o **-all**) con el comando **git help**: 

   git help -a


+ Configurar el nombre de usuario:

	git config --global user.name "*Nombre Apellido*"


+ Configurar el e-mail de usuario:

	git config --global user.email *email@dominio.extension*


+ Inicializar el repositorio:

	git init


+ Para ver el estado de los achivos del proyecto:

	git status


+ Ver los archivos no seguidos (comando de fontanería):

	git ls-files --others


+ Añadir un archivo al índice:

	git add *archivo*


+ Visualizar los archivos presentes en el índice y repositorio e identificarlos bajo la forma del hash que Git les ha asignado:

	git ls-files --stage


+ Guardar los archivos del indice en el repositorio:

	git commit -m "*mensaje*"


+ Ver los detalles del último commit (incluyendo el identificador hash):

	git log -1 


+ Mostrar los archivos que estan en el repositorio con su identificador.

	git ls-tree -r HEAD