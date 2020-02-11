---
title: Realizar copias de seguridad y restaurar bases de datos del sistema (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0259f14bb814fd4157af95e4ce92f462d1fab68a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62877282"
---
# <a name="back-up-and-restore-of-system-databases-sql-server"></a>Realizar copias de seguridad y restaurar bases de datos del sistema (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene un conjunto de bases de datos de nivel de sistema,*bases de datos del sistema*, esenciales para el funcionamiento de una instancia del servidor. Varias de las bases de datos del sistema requieren que se hagan copias de seguridad tras cualquier actualización de importancia. Las bases de datos del sistema de las que siempre debe realizar copias de seguridad son **msdb**, **maestra**y **model**. Si alguna base de datos utiliza la replicación en la instancia de servidor, existe la base de datos del sistema **distribution** de la que también debe hacer una copia de seguridad. La copia de seguridad de estas bases de datos del sistema le permite restaurar y recuperar el sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el caso de producirse un error del sistema, por ejemplo una pérdida del disco duro.  
  
 En la tabla siguiente se resumen todas las bases de datos del sistema.  
  
|Base de datos del sistema|Descripción|¿Son necesarias copias de seguridad?|modelo de recuperación|Comentarios|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[maestra](../databases/master-database.md)|Base de datos en la que se registra toda la información del sistema de un sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Sí|Simple|Realice copias de seguridad de la base de datos **maestra** con la frecuencia necesaria para que los datos estén suficientemente protegidos según sus necesidades empresariales. Se recomienda llevar a cabo una programación periódica de copias de seguridad, que se puede complementar con copias de seguridad adicionales cuando exista una actualización sustancial.|  
|[model](../databases/model-database.md)|Plantilla para todas las bases de datos creadas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sí|Configurable por el usuario<sup>1</sup>|Haga una copia de seguridad de **model** solo cuando sea necesario para sus necesidades empresariales: por ejemplo, después de personalizar las opciones de la base de datos.<br /><br /> **Recomendación:** es aconsejable crear copias de seguridad completas de base de datos de **model**, solo cuando sea necesario. Puesto que **model** es de pequeño tamaño y no suele cambiar, no es necesario realizar copia de seguridad del registro.|  
|[msdb](../databases/msdb-database.md)|La base de datos usada por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar alertas y trabajos y para registrar operadores. **msdb** también contiene tablas de historial y tablas de historial de copias de seguridad y restauración.|Sí|Simple (valor predeterminado)|Realice copias de seguridad de la base de datos **msdb** cuando se actualice.|  
|[Resource](../databases/resource-database.md) (RDB)|Base de datos de solo lectura que contiene copias de todos los objetos del sistema que se incluyen con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|No|-|La base de datos **Resource** se encuentra en el archivo mssqlsystemresource.mdf, que solo contiene código. Por lo tanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede hacer una copia de seguridad de la base de datos **Resource** .<br /><br /> Nota: Para realizar una copia de seguridad basada en archivos o basada en disco del archivo mssqlsystemresource.mdf, trátelo como si fuera un archivo binario (.exe), en lugar de un archivo de base de datos. No obstante, no puede utilizar la restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las copias de seguridad. La restauración de una copia de seguridad de mssqlsystemresource.mdf solo se puede hacer de forma manual y hay que tener cuidado de no sobrescribir la base de datos **Resource** actual con una versión obsoleta o potencialmente insegura.|  
|[tempdb](../databases/tempdb-database.md)|Área de trabajo que contiene conjuntos de resultados temporales o intermedios. Esta base de datos se vuelve a crear cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se cierra la instancia de servidor, los datos de la base de datos **tempdb** se eliminan de manera permanente.|No|Simple|No se pueden realizar copias de seguridad de la base de datos del sistema **tempdb** .|  
|[Configurar distribución](../replication/configure-distribution.md)|Base de datos que solo existe si el servidor está configurado como un distribuidor de replicación. En esta base de datos se almacenan metadatos y datos del historial de todos los tipos de replicación y transacciones de replicación transaccional.|Sí|Simple|Para obtener más información sobre cuándo realizar copias de seguridad de la base de datos **distribution** , vea [Hacer copias de seguridad y restaurar bases de datos replicadas](../replication/administration/back-up-and-restore-replicated-databases.md).|  
  
 <sup>1</sup> para obtener información sobre el modelo de recuperación actual del modelo, vea [ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md) o [sys. Databases &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
## <a name="limitations-on-restoring-system-databases"></a>Limitaciones sobre la restauración de las bases de datos del sistema  
  
-   Las bases de datos del sistema solo se pueden restaurar a partir de copias de seguridad creadas en la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en que se ejecuta actualmente la instancia de servidor. Por ejemplo, para restaurar una base de datos del sistema en una instancia de servidor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] que se ejecuta en SP1.  
  
-   Para restaurar una base de datos, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar ejecutándose. El inicio de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere el acceso a la base de datos **maestra** y la posibilidad de utilizarla al menos parcialmente. Si la base de datos **maestra** está inutilizable, puede devolverla a un estado válido de dos formas:  
  
    -   Restaure la base de datos **maestra** desde una copia de seguridad de la base de datos actual.  
  
         Si puede iniciar la instancia de servidor, debería poder restaurar la base de datos **maestra** desde una copia de seguridad completa de la base de datos.  
  
    -   Vuelva a generar la base de datos **maestra** completamente.  
  
         Si no puede iniciar **a causa de daños graves en la base de datos** maestra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deberá volver a generar la base de datos **maestra**. Para obtener más información, vea [Volver a generar bases de datos del sistema](../databases/system-databases.md).  
  
        > [!IMPORTANT]  
        >  Al recompilar la base de datos **maestra** , se recompilan todas las bases de datos del sistema.  
  
-   En algunas circunstancias, los problemas para recuperar la base de datos modelo pueden requerir la recompilación de las bases de datos del sistema o el reemplazo de los archivos mdf y ldf para la base de datos modelo. Para obtener más información, vea [Volver a generar bases de datos del sistema](../databases/system-databases.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](complete-database-restores-simple-recovery-model.md)  
  
-   [Restaurar la base de datos maestra &#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  
-   [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [Mover bases de datos del sistema](../databases/move-system-databases.md)  
  
## <a name="see-also"></a>Consulte también  
 [Base de datos de distribución](../../relational-databases/replication/distribution-database.md)   
 [Base de datos maestra](../databases/master-database.md)   
 [Base de datos msdb](../databases/msdb-database.md)   
 [Base de datos model](../databases/model-database.md)   
 [Base de datos Resource](../databases/resource-database.md)   
 [Base de datos tempdb](../databases/tempdb-database.md)  
  
  
