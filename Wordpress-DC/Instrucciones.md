### Puesta en Marcha

#### Pasos Iniciales

-   Configurar registros A & CName de dominio a IP del servidor.

-   Es recomendable no usar el usuario Root para las configuraciones iniciales, es por eso que vamos a crear un nuevo usuario root, para eso corre el siguiente comando (Servidor Ubuntu):

```bash
sudo adduser <nombre_del_usuario> --gecos "" --disabled-password && echo "<nombre_del_usuario>:<contraseña>" | sudo chpasswd && sudo usermod -aG sudo <nombre_del_usuario>
```

-   Este comando crea un nuevo usuario con el nombre especificado y lo agrega al grupo sudo, lo que le da al usuario permisos de root. La opción --gecos "" indica que no se agregue ninguna información adicional del usuario, y la opción --disabled-password asegura que el usuario no tenga una contraseña inicial.

-   Luego, se utiliza el comando echo junto con el nombre de usuario y contraseña para establecer la contraseña del usuario recién creado. Finalmente, el comando usermod se utiliza para agregar el nuevo usuario al grupo sudo.

-   Es importante tener en cuenta que otorgar a un usuario permisos de root puede ser peligroso, por lo que debes tener cuidado al crear y otorgar permisos de esta manera. Es recomendable solo otorgar permisos de root a usuarios confiables y para tareas específicas.

---

#### Posteriormente Seguir los siguientes pasos

1. Modificar en archivo nginx.conf your_domain & www.your_domain por tu dominio.
2. Definir credenciales de entorno en archivo .env
3. Cambiar los dominios name@your_domain, your_domain & www.your_domain en archivo docker-compose.yml
4. correr comando `docker-compose up -d`
5. Revisar que los contenedores esten corriendo con el comando `docker ps`
   Ej:

```bash
  Name                 Command               State           Ports
-------------------------------------------------------------------------
certbot     certbot certonly --webroot ...   Exit 0
db          docker-entrypoint.sh --def ...   Up       3306/tcp, 33060/tcp
webserver   nginx -g daemon off;             Up       0.0.0.0:80->80/tcp
wordpress   docker-entrypoint.sh php-fpm     Up       9000/tcp
```

5. Seguir Tutorial desde punto 5 <https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-docker-compose#step-5-modifying-the-web-server-configuration-and-service-definition>
