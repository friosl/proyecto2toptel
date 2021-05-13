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
   | Tiempo de respuesta | | |
   | Concurrencia | | |
   | CDN & Caching | | |
   | EFS | Amazon Elastic File System básicamente es un servicio de almacenamiento en la nube proporcionado por Amazon Web Services diseñado para proporcionar almacenamiento escalable, elástico, concurrente con algunas restricciones | Se creó la instancia del servicio EFS de Amazon y se montó a los servidores Vía IP |
