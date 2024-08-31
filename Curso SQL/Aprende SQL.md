**Qué es una base de datos?**
Una base de datos es todo lo que agrupe información y le dé un **sentido**

Para acceder a los datos en la base de datos se necesita usar un software llamado Relational Database Managment Sistem (RDBMS)
Tenemos a: MySQL, Postgres, MaríaDB, Oracle.
Estos software nos entregan un acceso fácil a nuestra base de datos, estos se encargan de la seguridad e integridad de nuestros datos, tienen funcionalidad para hacer respaldos de seguridad, importar, exportar, se encargan también de manejar la concurrencia que esto último vendría siendo que cuando más de una conexión está intentando entrar a la base de datos no haya inconsistencia.

También pueden conectarse con los distintos lenguajes de programación, lo más común que vamos a ver en bases de datos es el manejo de operaciones CRUD (CREATE, READ, UPDATE, DELETE).

Las aplicaciones giran entorno ala CRUD, para acceder a los registros y realizar todas las operaciones que tiene que hacer un sistema de bases de datos vamos a necesitar el query o consulta, es como: voy a realizar una petición o pregunta a mi base de datos de que si él puede crear el recurso que le estoy indicando que cree. Por ejemplo, cuando estamos buscando en google, estamos realizando un query.

Casi todas las empresas están usando software de gestión de bases de datos, por ejemplo Facebook que es una de las aplicaciones más complejas que existe actualmente, lo que hacen es que a través de un software de gestión de base de datos realizan consultas a la base de datos para poder obtener esta información, la cual se la devuelven al software y a su vez se le devuelve a la app de Facebook y finalmente tú la puedes ver.

Existen 2 mundos a la hora de seleccionar un gestor de base de datos, están los SQL y NoSQl
**SQL**
Suelen almacenar la información en forma de tablas con filas y columnas
**NoSQl**
Tienen múltiples formas de almacenar los datos, pueden ser almacenados en formato Json, Bson,Blod, etc.

En SQL se manejan tablas, con columnas y siendo las filas llamadas registro. Como vemos en esta tabla tiene ID y este es auto incrementable, ya que sería un número único de identificación.
![[Pasted image 20240825192707.png]]

Los valores que se encuentran dentro de las tablas son los datos pero cuando a toda la tabla se le asigna un nombre, es ahí cuando sabemos que todos los datos que están dentro de la tabla hacen referencia a algo es decir tienen sentido y es ahí cuando esto se convierte en información



