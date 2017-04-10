---
title: "Habilitar o deshabilitar sumas de comprobaci&#243;n de copia de seguridad durante copia de seguridad o restauraci&#243;n (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sumas de comprobación de copia de seguridad [SQL Server]"
  - "deshabilitar sumas de comprobación"
  - "sumas de comprobación [SQL Server]"
ms.assetid: 6786bd1e-ad97-430a-8dfb-d4ba952d6c4d
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# Habilitar o deshabilitar sumas de comprobaci&#243;n de copia de seguridad durante copia de seguridad o restauraci&#243;n (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo habilitar o deshabilitar sumas de comprobación de copia de seguridad cuando se realiza una copia de seguridad o se restaura una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para habilitar o deshabilitar sumas de comprobación de copias de seguridad, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 BACKUP  
 De forma predeterminada, los permisos BACKUP DATABASE y BACKUP LOG corresponden a los miembros del rol fijo de servidor **sysadmin** y de los roles fijos de base de datos **db_owner** y **db_backupoperator**.  
  
 Los problemas de propiedad y permisos del archivo físico del dispositivo de copia de seguridad pueden interferir con una operación de copia de seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe poder leer y escribir en el dispositivo y la cuenta en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos de escritura. Pero [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que agrega una entrada para un dispositivo de copia de seguridad en las tablas del sistema, no comprueba los permisos de acceso a los archivos. Es posible que estos problemas con el archivo físico del dispositivo de copia de seguridad no aparezcan hasta que se tenga acceso al recurso físico, al intentar la copia de seguridad o la restauración.  
  
 RESTORE  
 Si la base de datos que se va a restaurar no existe, el usuario debe tener permisos CREATE DATABASE para poder ejecutar RESTORE. Si la base de datos existe, los permisos RESTORE corresponden de forma predeterminada a los miembros de los roles fijos de servidor **sysadmin** y **dbcreator**, y al propietario (**dbo**) de la base de datos (para la opción FROM DATABASE_SNAPSHOT, la base de datos siempre existe).  
  
 Los permisos RESTORE se conceden a los roles en los que la información acerca de la pertenencia está siempre disponible para el servidor. Debido a que la pertenencia a un rol fijo de base de datos solo se puede comprobar cuando la base de datos es accesible y no está dañada, lo que no siempre ocurre cuando se ejecuta RESTORE, los miembros del rol fijo de base de datos **db_owner** no tienen permisos RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para habilitar o deshabilitar sumas de comprobación durante una operación de copia de seguridad  
  
1.  Siga los pasos para [crear una copia de seguridad de la base de datos](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  En la página **Opciones** , en la sección de **Confiabilidad** , haga clic en **Realizar suma de comprobación antes de escribir en los medios**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para habilitar o deshabilitar una suma de comprobación de copia de seguridad para una operación de copia de seguridad  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Para habilitar las sumas de comprobación de copia de seguridad en una instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md) , especifique la opción WITH CHECKSUM. Para deshabilitar sumas de comprobación de copia de seguridad, especifique la opción WITH NO_CHECKSUM. Es el comportamiento predeterminado, salvo para una copia de seguridad comprimida. En el siguiente ejemplo se especifica que se realicen sumas de comprobación.  
  
```tsql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
#### Para habilitar o deshabilitar una suma de comprobación de copia de seguridad para una operación de restauración  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Para habilitar las sumas de comprobación de copia de seguridad en una instrucción [RESTORE](../Topic/RESTORE%20\(Transact-SQL\).md) , especifique la opción WITH CHECKSUM. Es el comportamiento predeterminado para una copia de seguridad comprimida. Para deshabilitar sumas de comprobación de copia de seguridad, especifique la opción WITH NO_CHECKSUM. Es el comportamiento predeterminado, salvo para una copia de seguridad comprimida. En el siguiente ejemplo se especifica que se realicen sumas de comprobación de copia de seguridad.  
  
```tsql  
RESTORE DATABASE AdventureWorks2012   
 FROM DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH CHECKSUM;  
GO  
```  
  
> [!WARNING]  
>  Si solicita de forma explícita a CHECKSUM para una operación de restauración y la copia de seguridad contiene sumas de comprobación de copia de seguridad, se comprueban estas sumas y las sumas de comprobación de página, como en el caso predeterminado. No obstante, si el conjunto de copia de seguridad no tiene sumas de comprobación de copia de seguridad, la operación de restauración da error con un mensaje que indica que no hay sumas de comprobación.  
  
## Vea también  
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20LABELONLY%20\(Transact-SQL\).md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../Topic/RESTORE%20VERIFYONLY%20\(Transact-SQL\).md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE &#40;argumentos, Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)   
 [Errores posibles de medios durante copia de seguridad y restauración &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [Especificar si una operación de copia de seguridad o restauración continúa o se detiene después de encontrar un error &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
  