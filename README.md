***
# SISTEMA DE TOMA PEDIDO E INVENTARIO ARAMBALA CARAJO
***
## Configuracion del sistema para desarrolladores en entorno GNU/Linux.
### Funciona para Windows
***
### Configurar el backend
### Requisitos:
  1. PostgreSql 11
  2. JDK => 8
  3. Apache Maven => 3
  4. Eclipse IDE o cualquier otro.
***
### Configurar PostgreSql
#### 1. Crear el usuario de nuestra base de datos
```sql
CREATE ROLE arambalacarajo WITH ENCRYPTED PASSWORD 'contraseña';
```
#### 2. Crear la base de datos 
```sql
CREATE DATABASE arambalacarajo WITH OWNER arambalacarajo; 
```
#### 3. Agregar Roles de Usuario para el sistema.
```sql
 INSERT INTO role VALUES (1, 'Administrador'); 
 INSERT INTO role VALUES (2, 'Cajero'); 
 INSERT INTO role VALUES (3, 'Toma Pedido'); 
```
#### 4. Agregar un empleado
```sql
INSERT INTO empleados 
( cod_empleado, nombre , apellido, f_nacimiento, direccion,telefono, dui, activo, creado, actualizado) 
values 
('E-00001', 'Admin', 'Admin', '2019-03-10', 'El Salvador', '00000000','457856895', true, '2019-05-30', '2019-05-30'); 
```
```sql
 INSERT INTO usuario (id_usuario, nick, pass) 
 VALUES (1,'admin','$2a$10$Oyk1yfPfVK0lgKZUIvoh1e.xNRhyCdATvUJc0k1rVsoqrRapZodCO') 
```
```sql
INSERT INTO usuario_role (id_usuario_role, id_role,id_usuario) 
 VALUES(1, 1, 1); 
```
```sql
INSERT INTO usuario_empleado(id_usuario_empleado, id_usuario, cod_empleado)
VALUES(1,1,'E-00001');
```
##### Por defecto el usuario es: `admin` y la clave: `admin`, se recomienda cambiar la contraseña a una mas fuerte de una longitud mayor a 8 caracteres que contenga MAYUSCULAS y minusculas, asi como numeros y simbolos.

#### 5. Agregar categoria de menus
```sql
 INSERT INTO categoria
      VALUES
          (1, 'Alimentos', 'CA01'),
          (2,'Servicios','CS02'),
          (3,'Cabañas','CC03'); 

```
### Configurar proyecto
#### 1. Descargar el Backend
` git clone https://github.com/wilberArgueta/ArambalaCarajo-BACKEND.git`
#### 2. Moverlo al directorio de trabajo.
Linux: 
```bash
mv ArambalaCarajo-BACKEND/ /home/$USER/java-workspace/
```
#### 3. Configurar Spring Properties
Archivo de configuracion `src/main/resources/application.properties`
En `spring.datasource.password` agregar la contraseña para el rol `arambalacarajo`.
#### 4. Opcional configurar puerto del servidor.
Puerto por defecto `server.port = 9090`.
#### 5. Moverse a la raiz del proyecto y ejecutar Maven.
`mvn clean install`
***
### Configurar el FrontEnd
### Requisitos:
  1. NodeJS  => 10
  2. TypeScript => 3.0.0
  3. Angular => 6
***
#### 1. Descargar el FrontEnd
` git clone https://github.com/wilberArgueta/ArambalaCarajo-FRONTEND.git` 
#### 2. Instalar dependencias
En la raiz del proyecto ejecutar `npm install` y `npm update`
#### 3. Configurar el servidor
Modificar archivo `src/app/_class/backend.ts` y establecer el servidor que se ha configurado en el backend.
```javascript
export class Backend {
  constructor(public URL_BACKEND) {
    this.URL_BACKEND = 'http://localhost:9090';
  }
}
```
#### 4. Ejecutar el proyecto para corroborar que corre con los ajustes.
`ng serve --port 8080 -o`
