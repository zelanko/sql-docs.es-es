---
title: Recuperación de una base de datos sin restaurar los datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2109346c60ca807dcc818941f9baff862a211247
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126795"
---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>Recuperar una base de datos sin restaurar los datos (Transact-SQL)
  Normalmente, todos los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se restauran antes de que se recupere la base de datos. Sin embargo, una operación de restauración puede recuperar una base de datos sin restaurar realmente una copia de seguridad; por ejemplo, al recuperar un archivo de solo lectura que es coherente con la base de datos. Esto se conoce como *restauración de solo recuperación*. Cuando los datos sin conexión ya son coherentes con la base de datos y solo es necesario lograr que estén disponibles, una operación de solo restauración completa la recuperación de la base de datos y pone los datos en línea.  
  
 Una restauración de solo recuperación se puede realizar para una base de datos completa o para uno o varios archivos o grupos de archivos.  
  
## <a name="recovery-only-database-restore"></a>Restauración de solo recuperación de la base de datos  
 Una restauración de solo recuperación de base de datos puede resultar útil en las siguientes situaciones:  
  
-   No se recuperó la base de datos al restaurar la última copia de seguridad en una secuencia de restauración y ahora se desea recuperar la base de datos para ponerla en línea.  
  
-   La base de datos está en modo de espera y desea que se pueda actualizarla sin aplicar otra copia de seguridad de registros.  
  
 La sintaxis de [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para una restauración de solo recuperación de bases de datos es:  
  
 RESTORE DATABASE *database_name* WITH RECOVERY  
  
> [!NOTE]  
>  La cláusula FROM **=** \<*dispositivoDeCopiaDeSeguridad>* no se usa en las restauraciones de solo recuperación porque no es necesario realizar una copia de seguridad.  
  
 **Ejemplo**  
  
 En el siguiente ejemplo se recupera la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en una operación de restauración sin restaurar los datos.  
  
```  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## <a name="recovery-only-file-restore"></a>Restauración de solo recuperación  
 Una restauración de solo recuperación puede resultar útil en la siguiente situación:  
  
 Una base de datos se restaura por etapas. Una vez finalizada la restauración del grupo de archivos principal, uno o varios de los archivos no restaurados son coherentes con el nuevo estado de la base de datos; esto puede deberse a que la base de datos ha sido de solo lectura durante algún tiempo. Estos archivos solo necesitan recuperarse, no es necesario copiar los datos.  
  
 En una operación de restauración de solo recuperación los datos del grupo de archivos sin conexión pasan a estar en línea; no se produce ninguna fase de copia de datos, puesta al día ni reversión. Para obtener más información sobre las fases de restauración, vea [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md).  
  
 La sintaxis de [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para una restauración de solo recuperación de archivos es:  
  
 RESTORE DATABASE *database_name* { FILE **=**_logical_file_name_ | FILEGROUP **=**_logical_filegroup_name_ }[ **,**...*n* ] WITH RECOVERY  
  
 **Ejemplo**  
  
 En el siguiente ejemplo, se muestra una restauración de solo recuperación de archivos de los archivos de un grupo de archivos secundario, `SalesGroup2`, de la base de datos `Sales` . El grupo de archivos principal ya se ha restaurado como paso inicial de una restauración por etapas y `SalesGroup2` es coherente con el grupo de archivos principal restaurado. Recuperar este grupo de archivos y ponerlo en línea requiere una única instrucción.  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>Ejemplos de llevar a cabo una restauración por etapas con una restauración de solo recuperación  
 **Modelo de recuperación simple**  
  
-   [Ejemplo: Restauración por etapas de base de datos &#40;modelo de recuperación Simple&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: Restauración por etapas de sólo algunos grupos de archivos &#40;modelo de recuperación Simple&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **Modelo de recuperación completa**  
  
-   [Ejemplo: Restauración por etapas de base de datos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: Restauración por etapas de sólo algunos grupos de archivos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>Vea también  
 [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación simple&#41;](file-restores-simple-recovery-model.md)   
 [Restauraciones de archivos &#40;modelo de recuperación completa&#41;](file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
