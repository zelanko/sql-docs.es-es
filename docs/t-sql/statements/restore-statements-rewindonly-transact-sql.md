---
title: RESTORE REWINDONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- RESTORE_REWINDONLY_TSQL
- RESTORE REWINDONLY
dev_langs:
- TSQL
helpviewer_keywords:
- closing backup devices
- backup devices [SQL Server], rewinding
- media [SQL Server]
- open back devices
- rewinding backup devices
- RESTORE REWINDONLY statement
ms.assetid: 7f825b40-2264-4608-9809-590d0f09d882
caps.latest.revision: 50
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e1a07916c12d4043afd21daaa33cf77a222072f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="restore-statements---rewindonly-transact-sql"></a>Instrucciones RESTORE: REWINDONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rebobina y cierra los dispositivos de cinta especificados que se quedaron abiertos con las instrucciones BACKUP o RESTORE ejecutadas con la opción NOREWIND. Este comando solo se admite para dispositivos de cinta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RESTORE REWINDONLY   
FROM <backup_device> [ ,...n ]  
[ WITH {UNLOAD | NOUNLOAD}]  
}   
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | TAPE = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}   
```  
  
## <a name="arguments"></a>Argumentos  
 **\<backup_device> ::=** 
  
 Especifica los dispositivos de copia de seguridad físicos o lógicos que se utilizarán para la operación de restauración.  
  
 { *logical_backup_device_name* | **@***logical_backup_device_name_var* } es el nombre lógico, que debe seguir las reglas de los identificadores, del dispositivo de copia de seguridad creado por **sp_addumpdevice** desde el que se restaura la base de datos. Si se proporciona como una variable (**@***logical_backup_device_name_var*), el nombre del dispositivo de copia de seguridad se puede especificar como una constante de cadena (**@***logical_backup_device_name_var* = *logical_backup_device_name*) o como una variable de tipo de datos de cadena de caracteres, excepto los tipos de datos **ntext** o **text**.  
  
 {DISK | TAPE } **=** { **'***physical_backup_device_name***'** | **@***physical_backup_device_name_var* } permite restaurar las copias de seguridad guardadas en el dispositivo de disco o cinta con nombre. Los tipos de dispositivo de disco y cinta deben especificarse con el nombre real (por ejemplo, nombre de archivo y ruta de acceso completa) del dispositivo: DISK = 'C:\Archivos de programa\Microsoft SQL Server\MSSQL\BACKUP\Mybackup.bak' o TAPE = '\\\\.\TAPE0'. Si se especifica como una variable (**@***physical_backup_device_name_var*), el nombre del dispositivo se puede especificar como una constante de cadena (**@***physical_backup_device_name_var* = '* physical_backup_device_name*') o como una variable de tipo de datos de cadena de caracteres, excepto los tipos de datos **ntext** o **text**.  
  
 Si utiliza un servidor de red con un nombre UNC (que debe contener el nombre del equipo), especifique un tipo de dispositivo de disco. Para más información sobre cómo usar los nombres UNC, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 La cuenta en la que está ejecutando Microsoft SQL Server debe tener acceso de lectura al equipo remoto o servidor de red para poder realizar la operación RESTORE.  
  
 *n*  
 Marcador de posición que indica que se pueden especificar varios dispositivos de copia de seguridad y dispositivos lógicos de copia de seguridad. El número máximo de dispositivos de copia de seguridad o de dispositivos lógicos de copia de seguridad es **64**.  
  
 El hecho de que una secuencia de restauración requiera tantos dispositivos de copia de seguridad como los utilizados para crear el conjunto de medios al que pertenecen las copias de seguridad depende de si la restauración se realiza en línea o sin conexión. La restauración sin conexión permite restaurar una copia de seguridad con menos dispositivos que los utilizados para crear la copia de seguridad. La restauración en línea necesita todos los dispositivos de copia de seguridad para la copia de seguridad. Si se intenta la restauración con menos dispositivos, se obtiene un error.  
  
 Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
> [!NOTE]  
>  Si se restaura una copia de seguridad desde un conjunto de medios reflejado, solo puede especificar un reflejo para cada familia de medios. Pero, si hay errores, el hecho de tener otros reflejos habilita la resolución de algunos problemas de restauración rápidamente. Puede sustituir un volumen de medios dañado con el volumen correspondiente de otro reflejo. Tenga en cuenta que para las restauraciones sin conexión puede restaurar desde menos dispositivos que familias de medios, pero cada familia se procesa solo una vez.  
  
 **Opciones WITH**  
  
 UNLOAD  
 Especifica que la cinta se rebobine y se descargue automáticamente cuando termine una operación RESTORE. UNLOAD se establece de forma predeterminada al iniciar una nueva sesión de usuario. Permanece activo hasta que se especifica NOUNLOAD. Esta opción solo se utiliza para dispositivos de cinta. Si se utiliza para la operación de restauración un dispositivo que no es de cinta, esta opción no se tiene en cuenta.  
  
 NOUNLOAD  
 Especifica que la cinta no se descargue automáticamente de la unidad de cinta después de una operación RESTORE. NOUNLOAD permanece establecido hasta que se especifica UNLOAD.  
  
 Especifica que la cinta no se descargue automáticamente de la unidad de cinta después de una operación RESTORE. NOUNLOAD permanece establecido hasta que se especifica UNLOAD.  
  
## <a name="general-remarks"></a>Notas generales  
 RESTORE REWINDONLY es una alternativa a RESTORE LABELONLY FROM TAPE = \<nombre> WITH REWIND. Se puede encontrar una lista de las unidades de cinta abiertas si se consulta la vista de administración dinámica [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Cualquier usuario puede utilizar RESTORE REWINDONLY.  
  
## <a name="see-also"></a>Ver también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Historial de copias de seguridad e información de encabezados &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  

