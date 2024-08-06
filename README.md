# Server Docker
Para poder utilizarlo realicé una instalación de Lubuntu mínimal, luego instalé Docker y sobre éste instale Portainer para administrar los contenedores.
Tiene instalado dos discos duros de 4TB cada uno (aparte del que se utiliza para el SO) para almacenar los datos.

### Software instalado
- Cockpit para la administración del equipo, la instalación de actualizaciones, etc.
- Portainer para la administración de los otros contenedores.
- Jellyfin para la administración de la biblioteca multimedia (películas, series, música, colecciones de imágenes, etc.), permite el acceso a traves de la red con el navegador o con la aplicación correspondiente en el caso de los televisores y celulares.
- Nginx Reverse Proxy como bloqueador de anuncios y publicidad en los sitios web visitados sin la necesidad de instalar complementos en los navegadores, desgraciadamente no bloquea la publicidad de Youtube.
- OpenVPN para navegar a través de una red VPN para ciertos casos en que sea necesario, normalmente esta desactivado.

### Software instalado
Despues de la instalación se abre una consola y se ejecuta lo siguiente:

```php
#Verifico la configuración actual
sudo ip -4 address
#abro la configuración de la red con nano
sudo nano /etc/network/interfaces
#Edito o agrego las siguientes lineas, donde xxx es la ip que se le va a asignar al equipo
iface eno1 inet static
        address 192.168.0.xxx
        netmask 255.255.255.0
        network 192.168.0.0
        broadcast 192.168.0.255
        gateway 192.168.0.1
#reinicio el servicio de red
sudo systemctl restart networking
#Verifico la configuración actual, si esta todo bien se continua
sudo ip -4 address
#ajuste dependencias (opcional), algunas instalaciones dejan el dvd de instalación como sources, dando un error al tratar de actualizar
#comentar dvd sources
sudo nano /etc/apt/sources.list
#actualizar SO
sudo apt update
sudo apt upgrade
#instalación administrador web para el equipo
sudo apt install cockpit
sudo systemctl status cockpit
#instalar openssh y habilitar servicio ssh
sudo apt install openssh-server
sudo systemctl status ssh
sudo systemctl enable ssh
sudo systemctl start ssh
#Se puede activar o desactivar el entorno gráfico dependiendo de si es necesario o no
#Iniciar linux en modo gráfico
sudo systemctl set-default graphical.target
#Desactivar el entorno de escritorio en el inicio de Linux
sudo systemctl set-default multi-user.target
#instalación de docker
sudo apt install docker.io
#instalación de portainer
sudo docker volume create portainer_data
sudo docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
#repositorios portainer (opciones varias)
https://raw.githubusercontent.com/Lissy93/portainer-templates/main/templates.json
https://raw.githubusercontent.com/technorabilia/portainer-templates/main/lsio/templates/templates-2.0.json
https://raw.githubusercontent.com/ntv-one/portainer/main/template.json
https://raw.githubusercontent.com/portainer/templates/master/templates-2.0.json
```


## Licencia 📄
Este proyecto está bajo la Licencia GPL-3.0 license - ve el archivo [LICENSE](LICENSE) para detalles

## Contacto 📖
Puedes contactarte conmigo a través de cualquier de los siguientes canales:
- [Github](https://github.com/tenshi98)
- [Linkedin](https://www.linkedin.com/in/victor-reyes-galvez/)
- [Portafolio](https://tenshi98.github.io/portafolio/)
- [Mi Web](https://web.digitalcreations.cl/)

## Contribuciones 🎁
Si encontraste cualquier valor en este proyecto o quieres contribuir, aquí está lo que puedes hacer:

- Comparte este proyecto con otros.
- Invítame un café ☕.
- Inicia un nuevo problema o contribuye con un PR.
- Muestra tu agradecimiento diciendo gracias en un nuevo problema.

---

⌨️ por [Víctor Reyes](https://github.com/tenshi98) 😊