---
title: RESTORE VERIFYONLY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VERIFYONLY
- RESTORE VERIFYONLY
- VERIFYONLY_TSQL
- RESTORE_VERIFYONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE VERIFYONLY statement
- backups [SQL Server], verifying
- verifying backups
- checking backups
ms.assetid: cba3b6a0-b48e-4c94-812b-5b3cbb408bd6
caps.latest.revision: 64
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6996997ff66c291285fef4081dc7c21477ea8584
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="restore-statements---verifyonly-transact-sql"></a>Instrucciones - de RESTORE VERIFYONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comprueba la copia de seguridad, pero no la restaura, y comprueba si el conjunto de la copia de seguridad se ha completado y se puede leer en su totalidad. Sin embargo, RESTORE VERIFYONLY no intenta comprobar la estructura de los datos que contienen los volúmenes de la copia de seguridad. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], RESTORE VERIFYONLY se ha mejorado para realizar comprobaciones adicionales en los datos que se va a aumentar la probabilidad de detectar errores. El objetivo es acercarse lo máximo posible a una operación de restauración real de forma práctica. Para obtener más información, vea la sección Notas.  
  
 Si la copia de seguridad es válido, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] devuelve un mensaje de confirmación.  
  
> [!NOTE]  
>  Para ver descripciones de los argumentos, vea [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RESTORE VERIFYONLY  
FROM <backup_device> [ ,...n ]  
[ WITH    
 {  
   LOADHISTORY   
  
--Restore Operation Option  
 | MOVE 'logical_file_name_in_backup' TO 'operating_system_file_name'   
          [ ,...n ]   
  
--Backup Set Options  
 | FILE = { backup_set_file_number | @backup_set_file_number }   
 | PASSWORD = { password | @password_variable }   
  
--Media Set Options  
 | MEDIANAME = { media_name | @media_name_variable }   
 | MEDIAPASSWORD = { mediapassword | @mediapassword_variable }  
  
--Error Management Options  
 | { CHECKSUM | NO_CHECKSUM }   
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Monitoring Options  
 | STATS [ = percentage ]   
  
--Tape Options  
 | { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }    
 } [ ,...n ]  
]  
[;]  
  
<backup_device> ::=  
{   
   { logical_backup_device_name |  
      @logical_backup_device_name_var }  
   | { DISK | TAPE } = { 'physical_backup_device_name' |  
       @physical_backup_device_name_var }   
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 Ver las descripciones de los argumentos de RESTORE VERIFYONLY [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).  
  
## <a name="general-remarks"></a>Notas generales  
 El conjunto de medios o el conjunto de copia de seguridad debe contener la información mínima correcta para interpretarse como formato de cinta de Microsoft. Si no es así, RESTORE VERIFYONLY se detiene e indica que el formato de la copia de seguridad no es válido.  
  
 Entre las comprobaciones realizadas por RESTORE VERIFYONLY, se incluyen las siguientes:  
  
-   Que el conjunto de copia de seguridad ha finalizado y todos los volúmenes pueden leerse.  
  
-   Algunos campos de encabezado de páginas de base de datos, como el Id. de página (como si estuviera a punto de escribir los datos).  
  
-   Suma de comprobación (si está presente en los medios).  
  
-   Comprobar que existe espacio suficiente en los dispositivos de destino.  
  
> [!NOTE]  
>  RESTORE VERIFYONLY no funciona en una instantánea de base de datos. Para comprobar una instantánea de base de datos antes de realizar una operación de reversión, puede ejecutar DBCC CHECKDB.  
  
> [!NOTE]  
>  Con las copias de seguridad de instantánea, RESTORE VERIFYONLY confirma la existencia de las instantáneas en las ubicaciones especificadas en el archivo de copia de seguridad. Las copias de seguridad de instantánea son una característica nueva en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Para obtener más información acerca de las copias de seguridad de instantánea, vea [copias de seguridad de instantánea de archivos para archivos de base de datos en Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="security"></a>Seguridad  
 La operación de copia de seguridad puede especificar opcionalmente contraseñas de un conjunto de medios, de un conjunto de copia de seguridad o de ambos. Si se ha definido una contraseña en un conjunto de medios o un conjunto de copia de seguridad, debe especificar la contraseña o contraseñas correctas en la instrucción RESTORE. Estas contraseñas impiden operaciones de restauración y anexiones no autorizadas de los conjuntos de copia de seguridad en medios que utilizan herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, la contraseña no impide que se sobrescriba el medio con la opción FORMAT de la instrucción BACKUP.  
  
> [!IMPORTANT]  
>  El nivel de protección que proporciona esta contraseña es bajo. El objetivo es impedir una restauración incorrecta con las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya sea por parte de usuarios autorizados o no autorizados. No impide la lectura de los datos de las copias de seguridad por otros medios o el reemplazo de la contraseña. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]La práctica recomendada para proteger las copias de seguridad consiste en almacenar las cintas de copia de seguridad en una ubicación segura o copia de seguridad en archivos de disco que estén protegidos mediante listas de control de acceso adecuados (ACL). Las ACL se deben establecer en el directorio raíz en el que se crean las copias de seguridad.  
  
### <a name="permissions"></a>Permissions  
 A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], para obtener información sobre un conjunto de copia de seguridad o un dispositivo de copia de seguridad, es necesario el permiso CREATE DATABASE. Para obtener más información, vea [GRANT &#40;permisos de base de datos de Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Historial de copias de seguridad e información de encabezados &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
  
