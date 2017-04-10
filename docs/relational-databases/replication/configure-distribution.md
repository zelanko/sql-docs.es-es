---
title: "Configurar la distribuci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación [SQL Server], distribución"
  - "configuración de la distribución [replicación de SQL Server]"
  - "distribuidores remotos [replicación de SQL Server]"
  - "replicación transaccional, configurar distribución"
  - "bases de datos de distribución [SQL Server], ajustar tamaño"
  - "distribuidores [replicación de SQL Server], configurar"
  - "bases de datos de distribución [replicación de SQL Server], acerca de las bases de datos de distribución"
  - "bases de datos de distribución [SQL Server]"
  - "replicación de mezcla [replicación de SQL Server], configurar distribución"
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Configurar la distribuci&#243;n
  El distribuidor es un servidor que contiene la base de datos de distribución, que almacena metadatos y datos del historial de todos los tipos de replicación y transacciones para la replicación transaccional. Para configurar la replicación, debe configurar un distribuidor. Un publicador solamente se puede asignar a una instancia del distribuidor, aunque varios publicadores pueden compartir un distribuidor. El distribuidor utiliza estos recursos adicionales en el servidor en el que se encuentra:  
  
-   Espacio de disco adicional, si los archivos de instantáneas de la publicación se almacenan en el distribuidor (la situación habitual)  
  
-   Espacio de disco adicional para almacenar la base de datos de distribución.  
  
-   Uso adicional del procesador por los agentes de replicación para las suscripciones de inserción que se ejecutan en el distribuidor  
  
 El servidor seleccionado como distribuidor debe disponer del espacio en disco y la capacidad de proceso adecuados para la replicación y cualquier otra actividad asignada a ese servidor. Al configurar el distribuidor, debe especificar:  
  
-   Una carpeta de instantáneas que se utiliza, de manera predeterminada, para todos los publicadores que usen este distribuidor. Asegúrese de que la carpeta esté compartida y tenga establecidos los permisos adecuados. Para obtener más información, consulte [proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
-   El nombre y la ubicación de los archivos de la base de datos de distribución. No se puede cambiar el nombre de la base de datos de distribución una vez creada. Si desea utilizar un nombre distinto para la base de datos, debe deshabilitar la distribución y volver a configurar la base de datos.  
  
-   Todos los publicadores autorizados para utilizar el distribuidor. Si especifica otros publicadores además de la instancia en la que se ejecuta el distribuidor, debe especificar también una contraseña para las conexiones entre los publicadores y el distribuidor remoto.  
  
 Para la replicación transaccional después de configurar la distribución, se recomienda:  
  
-   Ajustar la base de datos de distribución a un tamaño apropiado. Pruebe la replicación con una carga típica para el sistema con el fin de determinar cuánto espacio se necesita para almacenar comandos. Asegúrese de que la base de datos es lo suficientemente grande para almacenar comandos sin recurrir al crecimiento automático con frecuencia. Para obtener más información acerca de cómo cambiar el tamaño de una base de datos, consulte [ALTER DATABASE & #40; Transact-SQL & #41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Configurar la opción **sync with backup** en la base de datos de distribución. Para obtener más información, consulte [estrategias para realizar copias de seguridad y restauración de instantáneas y transaccional](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md) y [Habilitar copias de seguridad coordinadas para la replicación transaccional & #40; Programación de replicación Transact-SQL & #41;](../../relational-databases/replication/administration/enable coordinated backups for transactional replication.md).  
  
## Distribuidores locales y remotos  
 De forma predeterminada, el distribuidor es el mismo servidor que el publicador (un distribuidor local), aunque también puede ser un servidor distinto del publicador (un distribuidor remoto). Por lo general, se elige un distribuidor remoto cuando se desea:  
  
-   Descargar el proceso en otro equipo para que la replicación tenga un impacto mínimo en el publicador (por ejemplo, si el publicador es un servidor OLTP).  
  
-   Configurar un distribuidor centralizado para varios publicadores.  
  
 Los distribuidores remotos son más frecuentes en la replicación transaccional que en la replicación de mezcla por dos motivos:  
  
-   El distribuidor tiene un rol más amplio en la replicación transaccional porque todas las transacciones replicadas se escriben y se leen en la base de datos de distribución.  
  
-   Las topologías de replicación de mezcla usan por lo general suscripciones de extracción, de forma que los agentes se ejecutan en cada suscriptor en lugar de ejecutarse todos en el distribuidor. Para obtener más información, consulte [suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md). En la mayoría de los casos, debe usar un distribuidor local para la replicación de mezcla.  
  
 Para configurar la publicación y la distribución, vea [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
 Para modificar las propiedades del distribuidor y del publicador, vea [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
## Vea también  
 [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  