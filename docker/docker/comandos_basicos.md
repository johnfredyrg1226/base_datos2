### docker-compose.yml


## primero para entrar
docker exec -it phpmyadmin sh


## ** docker exec -it mysql-db mysql -u root -p
MYSQL_ROOT_PASSWORD: rootpassword123

### levantar el contenedor docker compuse:

```sql
docker compose up -d
```


### reiniciar los contenedore

```sql
docker compose restart
```





### DETENER TODOS LOS CONTENEDORES 
```sql
docker stop $(docker ps -q)
```

docker stop mysql-db


### VER CONTENEDORES EN EJECUCION 

```sql
docker ps
```




### VER TODOS LOS CONTENEDORES 

```sql 

### REINICIAR CONTENEDOR 
```sql
docker restart <container_name_or_id>
```



### ELIMINAR CONTENEDOR
```sql
docker rm <container_name_or_id>
```



### ACCEDER UN CONTENEDOR EN EJECUCION TERNIMAL INTERACTIVA

```sql
docker exec -it <container_name_or_id> bash
```

### VER REGISTROS DE UN CONTENEDOR 

```sql
docker logs <container_name_or_id>
```


### VER PROCESOS DE EJECUCION EN UN CONTENEDOR 

```sql
docker top <container_name_or_id>
```

