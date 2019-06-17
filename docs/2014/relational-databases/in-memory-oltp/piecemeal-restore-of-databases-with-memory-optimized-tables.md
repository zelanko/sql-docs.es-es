---
title: Restauración por etapas de bases de datos con tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3c9ee00a81dd64ea1fa6093eaccc8d9b96e0aa59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806697"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>Restauración por etapas de bases de datos con tablas con optimización para memoria
  La restauración por etapas se admite en bases de datos con tablas optimizadas para memoria, a excepción de una restricción que describe más adelante. Para obtener más información sobre la restauración y la copia de seguridad por etapas, vea [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql) y [Restauraciones por etapas &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md).  
  
 La copia de seguridad y la restauración de un grupo de archivos principal y de un grupo de archivos optimizados para memoria deben realizarse conjuntamente:  
  
-   Si realiza una copia de seguridad (o restaura) el grupo de archivos principal, debe especificar el grupo de archivos optimizados para memoria.  
  
-   Si realiza una copia de seguridad (o restaura) el grupo de archivos optimizados para memoria, debe especificar el grupo de archivos principal.  
  
 Estos son los escenarios clave para la copia de seguridad y la restauración por etapas:  
  
-   La copia de seguridad por etapas permite reducir el tamaño de la copia de seguridad. He aquí algunos ejemplos:  
  
    -   Configure la copia de seguridad de la base de datos para que se realice a horas o en días diferentes con el fin de minimizar el impacto sobre la carga de trabajo. Un ejemplo es una base de datos muy grande (mayor de 1 TB) en la que no se puede completar una copia de seguridad completa de la base de datos en el tiempo asignado para el mantenimiento de bases de datos. En esa situación, puede usar la copia de seguridad por etapas para hacer copia de seguridad de toda la base de datos en varias copias de seguridad por etapas.  
  
    -   Si un grupo de archivos está marcado como de solo lectura, no requiere una copia de seguridad de registros de transacciones después de que se haya marcado como de solo lectura. Puede decidir realizar la copia de seguridad del grupo de archivos solo una vez después de marcarlo de solo lectura.  
  
-   Restauración por etapas.  
  
    -   El objetivo de una restauración por etapas es poner en línea las partes fundamentales de la base de datos sin esperar a todos los datos. Un ejemplo es si una base de datos tiene datos particionados, como los de particiones antiguas que se usan con poca frecuencia. Puede restaurar solo esos datos según sea necesario. Esto es similar para los grupos de archivos que contienen, por ejemplo, datos históricos.  
  
    -   Mediante la reparación de página, puede corregir daños en una página restaurando específicamente esa página. Para obtener más información, vea [Restaurar páginas &#40;SQL Server&#41;](../backup-restore/restore-pages-sql-server.md).  
  
## <a name="samples"></a>Muestras  
 En los ejemplos se usa el esquema siguiente:  
  
```  
CREATE DATABASE imoltp  
ON PRIMARY (name = imoltp_primary1, filename = 'c:\data\imoltp_data1.mdf')  
LOG ON (name = imoltp_log, filename = 'c:\data\imoltp_log.ldf')  
GO  
  
ALTER DATABASE imoltp ADD FILE (name = imoltp_primary2, filename = 'c:\data\imoltp_data2.ndf')  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_secondary  
ALTER DATABASE imoltp ADD FILE (name = imoltp_secondary, filename = 'c:\data\imoltp_secondary.ndf') TO FILEGROUP imoltp_secondary  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod2', filename='c:\data\imoltp_mod2') TO FILEGROUP imoltp_mod   
GO  
```  
  
### <a name="backup"></a>Copia de seguridad  
 En este ejemplo se muestra cómo hacer copia de seguridad del grupo de archivos principal y el grupo de archivos optimizados para memoria. Debe especificar juntos el grupo de archivos principal y el grupo de archivos optimizados para memoria.  
  
```  
backup database imoltp filegroup='primary', filegroup='imoltp_mod' to disk='c:\data\imoltp.dmp' with init  
```  
  
 En el ejemplo siguiente se muestra que una copia de seguridad de grupos de archivos que no son del grupo de archivos principal y optimizados para memoria es similar a las bases de datos que no tienen tablas optimizadas para memoria. El comando siguiente hace copia de seguridad hasta el grupo de archivos secundario  
  
```  
backup database imoltp filegroup='imoltp_secondary' to disk='c:\data\imoltp_secondary.dmp' with init  
```  
  
### <a name="restore"></a>Restaurar  
 En el ejemplo siguiente se muestra cómo restaurar conjuntamente el grupo de archivos principal y el grupo de archivos optimizados para memoria.  
  
```  
restore database imoltp filegroup = 'primary', filegroup = 'imoltp_mod'   
from disk='c:\data\imoltp.dmp' with partial, norecovery  
  
--restore the transaction log  
 RESTORE LOG [imoltp] FROM DISK = N'c:\data\imoltp_log.dmp' WITH  FILE = 1,  NOUNLOAD,  STATS = 10  
GO  
```  
  
 En el ejemplo siguiente se muestra que la restauración de grupos de archivos distintos del grupo de archivos principal y optimizado para memoria es similar a las bases de datos que no tienen tablas optimizadas para memoria.  
  
```  
RESTORE DATABASE [imoltp] FILE = N'imoltp_secondary'   
FROM  DISK = N'c:\data\imoltp_secondary.dmp' WITH  FILE = 1,  RECOVERY,  NOUNLOAD,  STATS = 10  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](../../database-engine/backup-restore-and-recovery-of-memory-optimized-tables.md)  
  
  
