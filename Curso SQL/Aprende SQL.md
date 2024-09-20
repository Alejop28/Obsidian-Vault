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

Los valores que se encuentran dentro de las tablas son los datos pero cuando a toda la tabla se le asigna un nombre, es ahí cuando sabemos que todos los datos que están dentro de la tabla hacen referencia a algo es decir tienen sentido y es ahí cuando esto se convierte en información.

Por lo general la tabla usuarios es la mas importante ya que mediante esta tabla vamos a poder asignarle los registros que se creen a alguien como
por ejemplo a continuación, con la tabla productos, podemos tener varios usuarios, administradores, usuarios que vayan a comprar etc.
Ahora vamos a ver el tipo admin
![[Pasted image 20240831224320.png]]

Todas las bases de datos SQL se mueven alrededor de este modelo; guardar un registro en una tabla, guardar otro en otra tabla y después asociarlos mediante alguna forma, en la tabla anterior vemos una relacion de 1->n (Uno a n)

Qué pasa cuando tenemos relaciones de n->n o muchos a muchos?
En estos casos lo mejor es crear una tabla intermedia 

![[Pasted image 20240831225000.png]]


Al hacer esta relación podemos haver uso de PK y FK 
![[Pasted image 20240831231949.png]]


Ya creada la base de datos en MYSQL tenemos:
![[Pasted image 20240901000507.png]]
Comando para crear la base de datos
Comando para ver las bases de datos
Comando para crear tablas
Las tablas deben tener un contenido, vamos  a darle columnas, por eso se le abre paréntesis y dentro de este se comienza a crear la tabla, cuando trabajamos con varchar también se le deben asignar paréntesis para indicarle cuantos dígitos soporta, cada variable se separa por ","
Para asignar la primary key y la tabla quede con su identificador único escribimos "PRIMARY KEY (id)" y entre paréntesis el nombre de la variable.

Hasta este punto la consulta no sabe qué base de datos utilizar, así que vamos a indicarle cual "use holamundo; "
![[Pasted image 20240901001307.png]]

Ahora vamos a ver cómo insertar datos dentro de esta tabla, se usa el INSERT INTO y VALUES:
`INSERT INTO aniamles(tipo,estado) VALUES ("chanchito","feliz");` 
Pero tenemos un error porque establecimos una primary key, pero no le dijimos que fuera auto incrementable, para eso se usa 
`ALTER TABLE animales MODIFY COLUMN id int aunto_increment;`

Ejemplo tabla con PK y FK:

`CREATE TABLE [Facturas](`

`[ID] INT NOT NULL IDENTITY (1,1),`
`[Num_Factura] INT NOT NULL,`
`[Cliente] INT NOT NULL,`
`[Metodo_Pago] INT NOT NULL,`
`[IVA] DECIMAL(18,2) NOT NULL,`
`[Total] DECIMAL(18,2) NOT NULL,`
`[Fecha] DATE DEFAULT GETDATE(),`

`CONSTRAINT [PK_Facturas] PRIMARY KEY CLUSTERED ([ID]),`
`CONSTRAINT [FK_Cliente] FOREIGN KEY ([Cliente]) REFERENCES [Clientes] ([ID]),`
`CONSTRAINT [FK_Metodo_Pago] FOREIGN KEY ([Metodo_Pago]) REFERENCES [Metodos_Pagos] ([ID])`
`)`
`GO`

Los valores se encierran en corchetes para poder utilizar en caso tal palabras reservadas:

Constraint: Son restricciones 
Clustered: Agrupaciones en memoria física
Quiere decir que la PK está restringida con el nombre dado y que se agrupan en el campo ID.
ejemplo INSERT Y SELECT

![[Pasted image 20240915203857.png]]

Aquí vemos como insertar y seleccionar datos específicos, podemos también hacer uso de AND y OR 

Funcionamiento de UPDATE:
![[Pasted image 20240915204447.png]]
Primero se ejecutó la línea y luego se ven registrados los cambios en la tabla.
DELETE:
`DELETE FROM Mascotas WHERE ID=5;`
Para borrar siempre el WHERE con un ID porque si no, hago un daño 

ALTER TABLE:
Ejemplo para modificar el tipo de dato

`ALTER TABLE CLIENTES ALTER COLUMN Celular NVARCHAR(15)`

El SELECT tiene varios usos, se pueden utilizar comandos como limit, que como su nombre indica limitaran el numero de registros y nos lo mostrará

`SELECT * FROM Clientes LIMIT 3`
Esto me mostrará los 3 primeros registros de Clientes que encuentre
También podemos utilizar operadores lógicos como (<,>,<=,>=,!=)

`SELECT * FROM Mascotas WHERE Especie != 'Gato' OR Peso>10`
También podemos usar:
`SELECT * FROM Mascotas WHERE Peso BETWEEN 2 AND 9
Esto me va a retornar los registros con un peso entre 2 y 9
`SELECT * FROM Clientes WHERE email like %gmail%`
Esto me va a mostrar todos los correos que sean gmail, sin importar que esté adelante o atrás de esta expresión, para eso los "% %"

-Podemos también organizar los datos de manera ascendente o descendente 
`SELECT * FROM Mascotas ORDER BY Peso asc` 
`SELECT * FROM Mascotas ORDER BY Peso desc` 

-Podemos seleccionar datos máximos y mínimos 
`SELECT MAX(Peso) AS Mayor FROM Clientes` 
`SELECT MIN(Peso) AS Menor FROM Clientes` 
El AS se usa para darle alias a ciertas columnas como lo vemos en el ejemplo anterior, este es mayormente utilizado con:
-MAX
-MIN
-GROUP BY (Agrupación de datos)




