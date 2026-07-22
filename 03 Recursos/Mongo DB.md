---
tags:
  - recurso
  - database
nivel: aprendiendo
---
#### [1.Inicia MongoDB](https://www.mongodb.com/es/docs/v7.0/tutorial/install-mongodb-on-debian/#start-mongodb "Permalink to this heading")

Puedes iniciar el proceso [`mongod`](https://www.mongodb.com/es/docs/v7.0/reference/program/mongod/#mongodb-binary-bin.mongod) emitiendo el siguiente comando:

```
sudo systemctl start mongod
```

Si recibe un error similar al siguiente al iniciar [`mongod`:](https://www.mongodb.com/es/docs/v7.0/reference/program/mongod/#mongodb-binary-bin.mongod)

`Failed to start mongod.service: Unit mongod.service not found.`

Ejecute primero el siguiente comando:

```
sudo systemctl daemon-reload
```

Luego ejecuta de nuevo el comando de inicio mencionado arriba.

#### [2.Verifica que MongoDB se haya iniciado correctamente](https://www.mongodb.com/es/docs/v7.0/tutorial/install-mongodb-on-debian/#verify-that-mongodb-has-started-successfully "Permalink to this heading")

```
sudo systemctl status mongod
```

Puedes asegurarte opcionalmente de que MongoDB se inicie después de un reinicio del sistema emitiendo el siguiente comando:

```
sudo systemctl enable mongod
```

#### [3.Detenga MongoDB](https://www.mongodb.com/es/docs/v7.0/tutorial/install-mongodb-on-debian/#stop-mongodb "Permalink to this heading")

Según sea necesario, puedes detener el proceso [`mongod`](https://www.mongodb.com/es/docs/v7.0/reference/program/mongod/#mongodb-binary-bin.mongod) ejecutando el siguiente comando:

```
sudo systemctl stop mongod
```

#### [4.Reinicia MongoDB](https://www.mongodb.com/es/docs/v7.0/tutorial/install-mongodb-on-debian/#restart-mongodb "Permalink to this heading")

Puedes reiniciar el proceso [`mongod`](https://www.mongodb.com/es/docs/v7.0/reference/program/mongod/#mongodb-binary-bin.mongod) emitiendo el siguiente comando:

```
sudo systemctl restart mongod
```

Puedes seguir el estado del proceso para detectar errores o mensajes importantes observando la salida en el archivo `/var/log/mongodb/mongod.log`.

#### [5.Comienza a utilizar MongoDB](https://www.mongodb.com/es/docs/v7.0/tutorial/install-mongodb-on-debian/#begin-using-mongodb "Permalink to this heading")

Inicia una [sesión`mongosh`](https://www.mongodb.com/es/docs/mongodb-shell/#mongodb-binary-bin.mongosh) en la misma máquina host que el [`mongod`](https://www.mongodb.com/es/docs/v7.0/reference/program/mongod/#mongodb-binary-bin.mongod). Puedes ejecutar [`mongosh`](https://www.mongodb.com/es/docs/mongodb-shell/#mongodb-binary-bin.mongosh) sin opciones de línea de comandos para conectarse a un [`mongod`](https://www.mongodb.com/es/docs/v7.0/reference/program/mongod/#mongodb-binary-bin.mongod) que se ejecuta en su localhost con el puerto por defecto 27017.

```
mongosh
```

## Usos actuales
- En la api [[]]