# PROYECTO 2 - TOPICOS DE TELEMATICA

## DOCUMENTACIÓN DE LA FASE DE ANÁLISIS Y DISEÑO
### SITIO WEB: https://www.reto1toptel.ml

## 1. Integrantes del Proyecto:
- Juan Felipe Londoño Gaviria
- Felipe Ríos López
- Juan David Pérez Sotelo

## 2. Roles: 
- Juan Felipe Londoño Gaviria - Rendimiento
- Felipe Ríos López - Disponibilidad
- Juan David Pérez Sotelo - Seguridad

## 3. Requisitos: 

### -  A. Requisitos Funcionales: 
  
   | Requisito | Descripcion | Implementacion |
   |------------|-------------|----------------|
   | | | |
   | | | |
   | | | |

### - B. Requisitos no Funcionales: 

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
    
   - Servidor DNS - CloudFlare y Freenom
   - CDN - CoudFlare
   - Balanceador de Cargas - AWS Load Balancer
   - Base de Datos - AWS RDS
   - Instacias de servidor Web & Bastion - AWS EC2 AMI Linux 2
   - Sistema de archivos - AWS EFS
   - Despliegue automatico para tolerancia a fallos - AWS AutoScaling
   - Manejo de redes y subredes - AWS VPC & Security Groups
   - Sistema de Monitoreo - CloudWatch


   ### - B. Patrones de Arquitectura:
   
   - Arquitectura en Capas (Las tres fundamentales serían: Capa de Negocio, Capa de Vista, Capa de Base de Datos)
   
