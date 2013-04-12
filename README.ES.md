Cómo hacer Git

Este artículo supone que Ud. bien entiende cómo usar la terminal OSX o Linux para cambiar entre directorios y mostrar sus contenidos usando los comandos `cd` y `ls`.

Es diferente usar Github y usar git. "git" en minúscula es cómo se llama el sistema de control de versiones (VCS o "version control system.") "Github" es un servicio web donde millones de repositorios git son colectados, y hay herramientas gráficas para examinarlos y compartirlos.

Por ejemplo, supone que estoy trabajando en un proyecto que se contiene en un repositorio, y hoy tengo la meta de añadir mi nombre en una lista de colaboradores en un archivo README.

1. Empezar con un cuento de Github. Tiene Ud. que saber su nombre usuario y su clave.

2. Navegar al directorio en su computadora donde Ud. quiere mantener proyectos. Yo tengo un directorio `/Users/ari/Projects/` donde se colocan todos mis pequeños proyectos. Dentro de aquí, recuerde que NO crea un directorio sólo por su nuevo proyecto, porque el comando `git clone` lo hará.

3. Navegar por un browser al URL del repositorio en Github. Ud. va a hacer un clon ("clone") del repositorio para que su computadora tiene una copia. Dentro de la terminal, toca al `git clone ` con espacio después de la palabra "clone" y esperar de tocar Enter.

Hacer clic sobre el botón "HTTP" en la página del repositorio. Copiar al portapapeles el URL del repositorio, que empieza con "https" y termine con ".git". Pegarlo después de `git clone`. Ahora sí puede Ud. tocar Enter.

Si tuviera un repositorio llamado "Treasury", esto parece: 

`$ git clone https://github.com/tensory/Treasury.git`

4. Navegar al nuevo directorio justo creado. Por mi ejemplo sería `/Users/ari/Projects/Treasury/`.

5. Crear un branch.

	__La Voz de Experiencia:__ Típicamente los tutoriales sobre git no empiezan con el concepto del branch. Yo creo que todos deben aprenderlo al primero. Entender eso, puede Ud. evitar muchos problemas con errores introducidos en el branch principal.

	Un branch es una versión del repositorio donde se puede hacer cambios sin cometerlos en el branch principal, que se llama "master". Si alguna vez no le gustan a Ud. los cambios que se han hechos al branch, puede Ud. borrarlo todo y empezar otra vez, sin causar ningún problema por master.

Pensar en un nombre para su nuevo branch que le ayudará recordar lo que intenta hacer con él. Es mejor crear un nuevo branch en cualquier momento que tiene una tarea específica para completar. Usar el comando `git checkout` para crear 