---
title: "Eliminar una instant&#225;nea de base de datos (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "quitar instantáneas de base de datos"
  - "eliminar instantáneas de base de datos"
  - "instantáneas de base de datos [SQL Server], eliminar"
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 35
---
# Eliminar una instant&#225;nea de base de datos (Transact-SQL)
  Al quitar una instantánea de base de datos, ésta se elimina de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se eliminan también los archivos dispersos que utiliza. Cuando se quita una instantánea de base de datos, se terminan también todas sus conexiones de usuario.  
  
## Seguridad  
  
###  <a name="Permissions"></a> Permisos  
 Cualquier usuario con permisos DROP DATABASE puede quitar una instantánea de base de datos.  
  
##  <a name="TsqlProcedure"></a> Quitar una instantánea de base de datos (mediante Transact-SQL)  
 **Para quitar una instantánea de base de datos**  
  
1.  Identifique la instantánea de base de datos que desee quitar. Puede ver las instantáneas de una base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Ver una instantánea de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
2.  Ejecute una instrucción [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) especificando el nombre de la instantánea de base de datos que se quitará. La sintaxis es la siguiente:  
  
     DROP DATABASE *nombre_de_instantánea_de_base_de_datos* [ **,**...*n* ]  
  
     Donde *nombre_de_instantánea_de_base_de_datos* es el nombre de la instantánea de base de datos que se va a quitar.  
  
####  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En este ejemplo se quita una instantánea de base de datos, denominada SalesSnapshot0600, sin que la base de datos de origen se vea afectada.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 Finalizan todas las conexiones de usuario a SalesSnapshot0600 y se eliminan todos los archivos dispersos del sistema de archivos NTFS que utiliza la instantánea.  
  
> [!NOTE]  
>  Para obtener más información sobre cómo las instantáneas de base de datos usan archivos dispersos, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear una instantánea de base de datos &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Ver una instantánea de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Revertir una base de datos a una instantánea de base de datos](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.png "Icono de flecha usado con el vínculo Volver al principio") [&#91;Principio&#93;](#Top)  
  
## Vea también  
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  