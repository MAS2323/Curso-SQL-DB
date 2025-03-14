#Bases de datos No-Sql 
### Pasas a seguir a la hora de disegnar una Base de Datos 
--- 1. Identificar los componentes que tendra nuestro sistema 
--- Ejemplo de bases de Datos para academias  educativas 
#### Campos o componentes 

```sh
Profesores 
Alumnos 
Cursos 
Notas 
Academia 
```

--- Una forma de evitar que algunos datos se repitan en nuestra bases de datos
--- es usando los id referidos mediante la relacion entre tablas 

```sh
Categoría	Tipo de Dato	Descripción
Numéricos	TINYINT	Número entero muy pequeño (rango: -128 a 127).
	SMALLINT	Número entero pequeño (rango: -32,768 a 32,767).
	MEDIUMINT	Número entero de tamaño mediano (rango: -8,388,608 a 8,388,607).
	INT	Número entero estándar (rango: -2,147,483,648 a 2,147,483,647).
	BIGINT	Número entero grande (rango: -9,223,372,036,854,775,808 a 9,223,372,036,854,775,807).
	DECIMAL	Número decimal con precisión fija, útil para datos financieros.
	NUMERIC	Sinónimo de DECIMAL.
	FLOAT	Número de punto flotante de precisión simple.
	DOUBLE	Número de punto flotante de precisión doble.
	BIT	Cadena de bits.
	UNSIGNED	Número entero sin signo (no permite valores negativos). Esto mejora mucho el rendimiento del propio campo.
Fecha y Hora	DATE	Fecha (YYYY-MM-DD).
	DATETIME	Fecha y hora (YYYY-MM-DD HH:MM:SS).
	TIMESTAMP	Marca de tiempo (YYYY-MM-DD HH:MM:SS).
	TIME	Hora (HH:MM:SS).
	YEAR	Año (AAAA).
Texto	CHAR	Cadena de texto de longitud fija.
	VARCHAR	Cadena de texto de longitud variable.
	TINYTEXT	Cadena de texto muy pequeña (hasta 255 caracteres).
	TEXT	Cadena de texto pequeña (hasta 65,535 caracteres).
	MEDIUMTEXT	Cadena de texto mediana (hasta 16,777,215 caracteres).
	LONGTEXT	Cadena de texto grande (hasta 4,294,967,295 caracteres).
	BINARY	Datos binarios de longitud fija.
	VARBINARY	Datos binarios de longitud variable.
	TINYBLOB	Datos binarios muy pequeños (hasta 255 bytes).
	BLOB	Datos binarios pequeños (hasta 65,535 bytes).
	MEDIUMBLOB	Datos binarios medianos (hasta 16,777,215 bytes).
	LONGBLOB	Datos binarios grandes (hasta 4,294,967,295 bytes).
	
		
```
### Tipos de Consultas SQL

#### Estructura de la Bases de Datos 

```sh

CREATE DATABASE -> Crear Bases de Dtos 
DROP DATABASE -> Eliminar Bases de Datos 
CREATE TABLE -> Crear Tablas 
ALTER TABLE -> Modificar Tablas 
DROP TABLE -> Eliminar Tablas 
```
#### Consultando y Modificando los Datos 

``sh 
SELECT -> Buscar  Bases de datos 
INSERT -> Agregar   ''
UPDATE -> Modificar   ''
DELETE -> Eliminar    ''
```

## Creacion de la Base de Datos 

--- Agregar Base de Datos 

```sh
CREATE DATABASE nombbre_data_base; 
```
### Eliminar Base de Datos 

```sh
DROP DATABASE IF EXISTS nombre_data_base; 
```

#### Comando para la creacion de Tablas:

```sh
CREATE TABLE usuarios(
id int(11) NOT NULL AUTO_INCREMENT,
nombre varchar(80) NOT NULL,
apellido varchar(80) NOT NULL,
fecha_nacimiento DATETIME NULL,
PRIMARY KEY (id)
);
```
#### Comando para la eliminacion de Tablas 

```sh
DROP TABLE IF EXISTS usuarios; 
```
## Comandos para modificar tablas 

#### Agregar Columnas 
```sh
ALTER TABLE usuarios ADD COLUMN telefono varchar(45) NULL;
```
#### Eliminar Columnas 
```sh
ALTER TABLE usuarios DROP telefono;
```
#### Mdificar Columnas
```sh
ALTER TABLE usuarios ALTER COLUMN telefono varchar(35) NULL;
```

### Comandos para Agregar y Eliminar Datos 

#### Comando para Agregar una Fila 

```sh 
INSERT INTO usuarios(
nombre, apellido, fecha_nacimiento,telefono)
VALUES('Lucas','Mas','1997-03-18 10:00:00', '12345678');
```
####Comando para Agregar una Fila 
```sh
#Siempre que estemos haciendo un delete no hay que olvidarse del FROM y de la 
#condicion WHERE 
DELETE FROM usuarios WHERE id = '1';
```

#### Modificar datos de una fila 

```sh 
#La sentencia UPDATE es como la sentencia DELETE siempre tiene que ir acompanado de un WHERER 

UPDATE usuarios 
SET nombre = 'ANTONIO',
apellido = 'MAS',
WHERE id = '1';
```	
## CONSULTAR Datos de nuestra Bases de Datos 

```sh
#Buscar todos los usuarios
# el asterisco hace que nos traigan todos los datos de la tabla usuarios de nuestra DB 
SELECT*FROM usuarios;
#Buscar el usuario con id 1
SELECT*FROM usurios WHERE id = '1';

# si queremos obtener captos especificos de nuestra tabla hacemos lo siguiente 
 SELECT id, apellido FROM usuarios; 

#Buscar el nombre y apellido del usuario 
SELECT nombre, apellido
FROM usuris WHERE id = '1';
```

### metodo Count 
```sh 
#Usamos este metodo para contar valores en nuestra base de datos

SELECT COUNT(*) FROM usuarios;
# esta sentencia sql nos devolvera cuantos elementos hay en la tabla usuarios 
```

### Hacer una seleccion o una busqueda en nuestra tabla en funcion a una condicion usando LIKE 

```sh
SELECT * FROM usuarios 
WHERER nombre LIKE 'lucas%'

# usamos simbolos como % delante o detras de la palabro que queremos encontrar o inicial de las palabras que queremos encontrar 

SELECT * FROM usuarios 
WHERER nombre LIKE '%l%'
# Esta consulta nos traera todos los nombres que se encuentren en nuestra tabla y contengan la letra L 
# podemos cambiar esta condicion 
```
### Optimizando la instruccion LIKE 
--- Cuando tengamos muchos datos en nuestra bases de datos no sera necesario poner el signo de % al principio de la palabra o letra clave, con ponerlo al final basta eso hace mas rapido la DB 

### La instruccion WHERE funciona igual tanto para el SELECT, DELETE y el UPDATE

```sh
# Actualizar un usuario ennuestra tabla cursos
UPDATE usuarios 
SET nombre = 'Pepe',
apellido = 'Ugano'
WHERER nombre LIKE '%l%'
```

```sh 
# Eliminar un usuario en nuestra tabla 
DLETE FROM usuarios 
WHERE apellido LIKE 'o%';
```
### Algunas consultas complejas en nuestra DB 

```sh 
# la instruccion CONCAT sirve para concatenar el el nombre y el apellido para que  al realizar la consulta no obtengamos dos tablas sino una linea 

# en esta consulata estaremos haciendola en dos tablas, para abreviar el nombre de nuestras tablas podemos usar cualquier letra que queramos o combinavion 
# en nuestro ejempo hemos usado p y u 
SELECT p.*,
CONCAT(u.nombre,'',u.apellido) as 'autor'
FROM publicaciones p, usuarios u
WHERE p.autor_id = u.id;
```
### Cosas a tener en cuenta 
--- A la hora de hacer este tipo de consultas no es recomendable utilizar la instruccion WHERE para establecer la condicion porque no es optimo  lo mas recomendable es utilizar los JOIN 

### INNER JOIN 

```sh
SELECT p.id,
p.titulo,
p.texto,
CONCAT(u.nombre,'',u.apellido) as 'autor'
FROM publicaciones p INNER JOIN usuarios u
ON p.autor_id = u.id;
```

```sh 
-- SQL Para Estadisticas 
-- FUNCION             DESCRIPCION
-- COUNT(*)            Cuenta la cantidad de filas 
-- MAX(puntaje)       Devuelve el maximo puntaje 
-- MIN(puntaje)     Devuelve el minimo puntaje 
-- AVG(puntaje)     Devuelve el puntaje promedio 
-- SUM(precio)         Devuelve una suma de precios
```
	```sh 
	mysql> SELECT * FROM productos;
+----+------------+--------+
| id | nombre     | precio |
+----+------------+--------+
|  1 | Zapatilla  |     30 |
|  2 | Pantalones |     45 |
|  3 | Camisa     |     23 |
|  4 | Perfume    |     33 |
+----+------------+--------+
4 rows in set (0.00 sec)

mysql> SELECT COUNT(*) FROM productos;
+----------+
| COUNT(*) |
+----------+
|        4 |
+----------+
1 row in set (0.00 sec)

mysql> SELECT MAX(precio) FROM productos;
+-------------+
| MAX(precio) |
+-------------+
|          45 |
+-------------+
1 row in set (0.00 sec)

mysql> SELECT MIN(precio) FROM productos;
+-------------+
| MIN(precio) |
+-------------+
|          23 |
+-------------+
1 row in set (0.00 sec)

mysql> SELECT AVG(precio) FROM productos;
+-------------+
| AVG(precio) |
+-------------+
|       32.75 |
+-------------+
1 row in set (0.00 sec)

mysql> SELECT SUM(precio) FROM productos;
+-------------+
| SUM(precio) |
+-------------+
|         131 |
+-------------+
1 row in set (0.00 sec)
```
##  SUBCONSULTAS EN SQL 

```sh
# Estas son ejemplos de subconsultas simples, esto se puede volver muy complejo dependiendo de las necesidades de creador 
-- En esta consulta nos traeran a todos las publicaciones cuyo nombre de autores 
-- contengan una m 
SELECT * FROM curso.publicaciones WHERE autor_id IN (
SELECT id FROM curso.usuarios WHERE nombre LIKE 'M%'
);

-- En esta consulta nos traeran a todos las publicaciones cuyo nombre de autores 
-- no contengan una m 
SELECT * FROM curso.publicaciones WHERE autor_id NOT IN (
SELECT id FROM curso.usuarios WHERE nombre LIKE 'M%'
);
```
### Agrupacion de consultas 
```sh
# podemos hacer unos UNION  esto

SELECT * FROM curso.usuarios WHERE nombre LIKE 'M%'
UNION
SELECT * FROM curso.usuarios WHERE nombre LIKE 'l%';
```
## GROUP BY 
### se usa esta consulta para agrupar en funcion a una condicion 

```sh
-- GROUP BY 
-- La funcion del GROUP BY es la de no reetir un valor si se encuentra mas 
-- de una ves en la columna seleccionada 
SELECT * FROM curso.usuarios GROUP BY nombre;
SELECT apellido, COUNT(*) AS total_usuarios
FROM curso.usuarios
GROUP BY apellido;
```
--- La consulta GROUP BY es mas util cuando estamos trabajndo con fechas
-- si quereos hacer una agrupacion en funcion a una fecha 


```sh
-- GROUP BY 
-- La funcion del GROUP BY es la de no reetir un valor si se encuentra mas 
-- de una ves en la columna seleccionada 
SELECT * FROM curso.usuarios GROUP BY nombre;
SELECT apellido, COUNT(*) AS total_usuarios
FROM curso.usuarios
GROUP BY apellido;
```

