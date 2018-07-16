---
title: 'Ejemplo: Restauración en línea de un archivo de lectura/escritura (modelo de recuperación completa) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- online restores [SQL Server], full recovery model
- restore sequences [SQL Server], online
ms.assetid: 0dbeda81-1464-44ba-9011-914900096368
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b139c9173a87e6b7c05c1abcf4d1a7e4c343ec4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307945"
---
# <a name="example-online-restore-of-a-read-write-file-full-recovery-model"></a>Ejemplo: Restauración en línea de un archivo de lectura/escritura (modelo de recuperación completa)
  Este tema solo es de interés para las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contengan varios archivos o grupos de archivos con el modelo de recuperación completa.  
  
 En este ejemplo, una base de datos llamada `adb`, que utiliza el modelo de recuperación completa, contiene tres grupos de archivos. El grupo de archivos `A` es de lectura/escritura, mientras que los grupos de archivos `B` y `C` son de solo lectura. Inicialmente, todos los grupos de archivos están en línea.  
  
 El archivo `a1` del grupo de archivos `A` está dañado y el administrador de la base de datos decide restaurarlo con la base de datos en línea.  
  
> [!NOTE]  
>  Con el modelo de recuperación simple no se puede realizar una restauración en línea de datos de lectura/escritura.  
  
## <a name="restore-sequences"></a>Secuencias de restauración  
  
> [!NOTE]  
>  La sintaxis de un flujo de restauración en línea es la misma que la de un flujo de restauración sin conexión.  
  
1.  Restauración en línea del archivo `a1`.  
  
    ```  
    RESTORE DATABASE adb FILE='a1' FROM backup   
    WITH NORECOVERY;  
    ```  
  
     En este momento, el archivo a1 se encuentra en el estado RESTORING, mientras que el grupo de archivos A está sin conexión.  
  
2.  Tras restaurar el archivo, el administrador de la base de datos realiza una nueva copia de seguridad de registros para asegurarse de capturar el momento en el que el archivo se quedó sin conexión.  
  
    ```  
    BACKUP LOG adb TO log_backup3;   
    ```  
  
3.  Restauración en línea de las copias de seguridad de registros.  
  
     El administrador restaura todas las copias de seguridad de registros tomadas desde la copia de seguridad de archivos restaurada, finalizando con la última copia de seguridad de registros (*log_backup3*, tomada en el paso 2). Tras restaurar la última copia de seguridad, la base de datos se recupera.  
  
    ```  
    RESTORE LOG adb FROM log_backup1 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup2 WITH NORECOVERY;  
    RESTORE LOG adb FROM log_backup3 WITH NORECOVERY;  
    RESTORE LOG adb WITH RECOVERY;  
    ```  
  
     Ahora el archivo `a1` está en línea.  
  
## <a name="additional-examples"></a>Otros ejemplos  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación simple&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración en línea de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vea también  
 [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Aplicar copias de seguridad de registros de transacción &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
