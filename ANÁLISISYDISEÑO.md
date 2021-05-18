|![http://www.eafit.edu.co/firmadigital/logo-EAFIT-color-Firma2015.jpg](documentacion/Aspose.Words.14d04a4b-8e63-451d-ab08-205d0e9c81ee.001.jpeg)|<p>**Escuela de ingeniería** </p><p>**Departamento de informática y sistemas**</p><p></p>||
| :- | :- | -: |
# PROYECTO 2 - TOPICOS DE TELEMATICA

## DOCUMENTACIÓN DE LA FASE DE ANÁLISIS Y DISEÑO
### SITIO WEB: https://www.certificado2.ml

## 1. Integrantes del Proyecto:
- Juan Felipe Londoño Gaviria
- Felipe Ríos López
- Juan David Pérez Sotelo

## 2. Roles: 
- Juan Felipe Londoño Gaviria - Rendimiento
- Felipe Ríos López - Disponibilidad
- Juan David Pérez Sotelo - Seguridad

## 3. Requisitos: 

### - A. Requisitos no Funcionales: 

   - Disponibilidad: 
   
   | Requisito | Descripcion | Implementacion |
   |------------|-------------|----------------|
   | Sistema de monitoreo | Se encarga de recopilar los datos con el cual se revisan los recursos que están corriendo | Se utilizó CloudWatch para la implementación del sistema de monitoreo y se configura la opción en el AutoScaling group |
   | Balanceador de carga | Se encarga de direccionar a un cliente al servidor web que se encuentre con mayor disponibilidad entre los que cuentan con el mismo contenido.| Se utilizó la herramienta de EC2  "Load Balancers" para crear las necesarias para la realización del proyecto |
   | Crecimiento Horizontal de Servidores | Dos zonas de Disponibilidad A - B| Se tiene un AutoScaling group que tiene mínimo 2 servidores, máximo 3, y con capacidad de CPU del 60%|
   | Disponibilidad en capa de servicios | Sirve para la conversión de las direcciones de red (NAT) para permitir a las instancias de la subred privada conectarse a Internet o a otros servicios | Se creó una imagen NAT de AMI de la comunidad para proveer este servicio |
   
   - Rendimiento:
     
   | Requisito | Descripcion | Implementacion |
   |------------|-------------|----------------|
   | CDN & Caching | Es una plataforma de servidores altamente distribuida que ayuda a minimizar los retrasos en la carga de contenidos de páginas web al reducir la distancia física entre el servidor y el usuario. | Se delegó el manejo de servicios del DNS desde el Freenom hasta el CloudFlare |
   | EFS | Amazon Elastic File System básicamente es un servicio de almacenamiento en la nube proporcionado por Amazon Web Services diseñado para proporcionar almacenamiento escalable, elástico, concurrente con algunas restricciones | Se creó la instancia del servicio EFS de Amazon y se montó a los servidores Vía IP |
   
   
   - Seguridad: 
 
   | Requisito | Descripcion | Implementacion |
   |------------|-------------|----------------|
   | Redes Privadas | Conjunto de direcciones donde estarán ubicadas las redes Privadas | Se definieron dos conjuntos de direcciones para redes privadas una para la zona de disponiblidad de A (172.31.1.0/24) y otra para B (172.31.3.0/24) |
   | Autenticación de doble factor | Es una herramienta que consta de 2 pasos para loguearse en la página web | Se descargó el PlugIn de WordPress llamado: WP 2FA – Two-factor Authentication for WordPress |
   | Bastion Host | Máquina desplegada en la zona pública que posee una conexión con las máquinas de la página ubicadas en la zona Privada | Se utilizan dos máquinas AMI para cada zona de Disponibilidad con una IP pública |
   | Manejo del protocolo HTTPS | El manejo consta de la definición de los certificados válidos para la página web | Se designaron los certificados WildCard utilizando CertBot |
   | Certificado WildCard |Es un certificado comodin de clave pública que se puede utilizar con varios subdominios de un dominio | Se solicitó el Certificado Wildcard desde Let's Encrypt por medio de CertBot para el dominio *.reto1toptel.ml 
   
   ## 4. Diseño Escalable
   
   ### - A. Herramientas utilizadas:
    
   - Servidor DNS - CloudFlare y Freenom: Cloudflare actúa como intermediaria entre el cliente y el servidor, usando unos sistemas llamados proxies reversos (reverse proxies) para crear copias espejo y cachés de sitios web, mientras que Freenom es el proovedor del dominio .ml
   
   - CDN - CoudFlare
   
   - Balanceador de Cargas - AWS Load Balancer: Elastic Load Balancing ofrece la capacidad para balancear cargas entre recursos locales y de AWS con un único balanceador de carga. Puede lograr esto al registrar todos sus recursos en el mismo grupo de destino y asociar dicho grupo con un balanceador de carga.
  
  - Base de Datos - AWS RDS:  El servicio suministra capacidad rentable y escalable al mismo tiempo que automatiza las arduas tareas administrativas, como el aprovisionamiento de hardware, la configuración de bases de datos, la implementación de parches y la creación de copias de seguridad. Lo libera de estas tareas para que pueda concentrarse en sus aplicaciones y darles el rendimiento rápido, la alta disponibilidad, la seguridad y la compatibilidad que necesitan.
   
   - Instacias de servidor Web & Bastion - AWS EC2 AMI Linux 2: Una instancia es un servidor virtual en la nube de AWS. Con Amazon EC2, puede instalar y configurar el sistema operativo y las aplicaciones que se ejecutan en la instancia.
   
   - Sistema de archivos - AWS EFS: Es un sistema de archivos elástico, sencillo, sin servidor, con posibilidad de establecer y olvidar y que permite compartir datos de archivos sin necesidad de aprovisionar o administrar el almacenamiento. Se puede utilizar con los servicios en la nube de AWS y con los recursos en las instalaciones y está diseñado para escalar bajo demanda a petabytes sin interrumpir las aplicaciones.
   
   - Despliegue automatico para tolerancia a fallos - AWS AutoScaling: AWS Auto Scaling le permite crear planes de escalado que automatizan la manera en la que diferentes recursos responden ante los cambios que se producen en la demanda
   
   - Manejo de redes y subredes - AWS VPC & Security Groups: Los security groups son grupos de seguridad que funcionan como un firewall virtual para las instancias EC2 para controlar el tráfico entrante y saliente y el VPC es un servicio que permite lanzar recursos de AWS en una red virtual aislada de forma lógica que usted defina. Puede controlar todos los aspectos del entorno de red virtual, como la selección de su propio rango de direcciones IP, la creación de subredes y la configuración de tablas de enrutamiento y gateways de red.
   
   - Sistema de Monitoreo - CloudWatch: Es un servicio que recopila datos de monitorización y operaciones en formato de registros, métricas y eventos, y permite su visualización mediante paneles automatizados para obtener una vista unificada de los recursos, las aplicaciones y los servicios de AWS que se ejecutan en servidores locales y de AWS.


   ### - B. Patrones de Arquitectura:
   
   - Arquitectura en Capas (Las tres fundamentales serían: Capa de Negocio, Capa de Vista, Capa de Base de Datos)
   - Arquitectura orientada a servicios (Puesto que consumimos un montón de servicios de AWS con el fin de resolver un objetivo en común)


   ### - C. Selección de Tácticas:

   - Stateless
   - Compresión de Archivos
   - Red de Distribución contenidos (CDN)


   ### - D. Mejores Prácticas:
   
   - Tomar en cuenta la teoría de colores para la parte estética. 
   - Reducir la cantidad de clicks para realizar una acción.
   - Tener redundancia en los datos
   - Usar CDN para mayor cobertura en diferentes zonas
   - Multiplicar el servicio de base de datos en múltiples zonas por la disponibilidad 
   - Crear servidores de archivos en caché 
   - Encriptar mensajes que envía internamente la página

  ## 5. Prueba de Disponibilidad
  
  ![DISPONIBILIDAD](https://i.imgur.com/eX6rsgO.jpeg)
   
