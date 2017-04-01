---
title: "Tutorial: copias de seguridad y restauraci&#243;n de SQL Server en el servicio de almacenamiento Blob de Windows Azure | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016 Preview"
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tutorial: copias de seguridad y restauraci&#243;n de SQL Server en el servicio de almacenamiento Blob de Windows Azure
Este es el tutorial Introducción a las copias de seguridad y la restauración de SQL Server con el servicio de almacenamiento Blob de Windows Azure. Este tutorial le ayudará a entender cómo escribir copias de seguridad en el servicio almacenamiento Blob de Windows Azure y cómo restaurar desde el mismo.  
  
## Aprendizaje  
Este tutorial muestra cómo crear una cuenta de almacenamiento de Windows, un contenedor de blobs, crear credenciales para tener acceso a la cuenta de almacenamiento, escribir una copia de seguridad en el servicio de blob y realizar una restauración simple. El tutorial está compuesto por cuatro lecciones:  
  
[Lección 1: Crear objetos de almacenamiento de Windows Azure](../Topic/Lesson%201:%20Create%20Windows%20Azure%20Storage%20Objects.md)  
En esta lección, creará una cuenta de almacenamiento de Windows Azure y un contenedor de blobs.  
  
[Lección 2: Crear una credencial de SQL Server](../Topic/Lesson%202:%20Create%20a%20SQL%20Server%20Credential.md)  
En esta lección, creará una credencial para almacenar la información de seguridad usada para tener acceso a la cuenta de almacenamiento de Windows Azure.  
  
[Lección 3: Escribir una copia de seguridad completa de la base de datos en el servicio de almacenamiento Blob de Windows Azure](../Topic/Lesson%203:%20Write%20a%20Full%20Database%20Backup%20to%20the%20Windows%20Azure%20Blob%20Storage%20Service.md)  
En esta lección, emitirá una instrucción T-SQL para escribir una copia de seguridad de la base de datos AdventureWorks2012 en el servicio de almacenamiento Blob de Windows Azure.  
  
[Lección 4: Realizar una restauración desde una copia de seguridad completa de la base de datos](../Topic/Lesson%204:%20Perform%20a%20Restore%20From%20a%20Full%20Database%20Backup.md)  
En esta lección, emitirá una instrucción T-SQL para restaurar desde la copia de seguridad de la base de datos creada en la lección anterior.  
  
### Requisitos  
Para completar este tutorial, debe estar familiarizado con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de copia de seguridad y restaurar los conceptos y la sintaxis de T-SQL. Para usar este tutorial, el sistema debe cumplir los requisitos siguientes:  
  
-   Una instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]y la base de datos AdventureWorks2012 instalada.  
  
    La instancia de SQL Server puede ser local o residir en una máquina virtual de Windows Azure.  
  
    Puede usar una base de datos de usuario en lugar de AdventureWorks2012 y modificar la sintaxis de tsql en consecuencia.  
  
-   La cuenta de usuario que se usa para emitir comandos BACKUP o RESTORE debe tener el rol de base de datos **operador de db_backup** con permisos **Modificar cualquier credencial**.  
  
### Lecturas adicionales  
A continuación se indican algunas lecturas recomendadas para entender los conceptos y las prácticas recomendadas cuando se usa el servicio de almacenamiento Blob de Windows Azure para copias de seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
1.  [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## Vea también  
[Realizar una copia de seguridad de la base de datos y el registro](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#databaselog)  
[Crear una copia de seguridad de archivos completa del grupo de archivos principal](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#filegroups)  
[Restaurar una base de datos y mover archivos](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#restoredbwithmove)  
  
