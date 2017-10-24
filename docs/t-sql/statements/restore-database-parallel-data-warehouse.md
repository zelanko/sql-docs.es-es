---
title: Restaurar base de datos (almacenamiento de datos en paralelo) | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 001813cf0e7d00e089046d8580108eb10ef4cba0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="restore-database-parallel-data-warehouse"></a>Restaurar base de datos (almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Restaura una [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] base de datos de usuario desde una copia de seguridad de base de datos en un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo. La base de datos se restaura desde una copia de seguridad que se creó anteriormente mediante el [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [copia de seguridad de la base de datos &#40; Almacenamiento de datos en paralelo &#41; ](../../t-sql/statements/backup-database-parallel-data-warehouse.md) comando. Utilice la copia de seguridad y restaurar las operaciones para crear un plan de recuperación ante desastres o para mover las bases de datos de un dispositivo a otro.  
  
> [!NOTE]  
>  Restaurar maestro incluye la restauración de información de inicio de sesión del dispositivo. Para restaurar la maestra, use la [restaurar la base de datos maestra &#40; Transact-SQL &#41; ](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) página en el **Configuration Manager** herramienta. Un administrador con acceso al nodo de Control puede realizar esta operación.  
  
 Para obtener más información acerca de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] copias de seguridad de base de datos, vea "Copia de seguridad y restauración" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 Restaurar base de datos *database_name*  
 Especifica que se debe restaurar una base de datos de usuario a una base de datos denominada *database_name*. La base de datos restaurada puede tener un nombre diferente de la base de datos de origen que se copió. *database_name* no puede existir como una base de datos en el dispositivo de destino. Para obtener más detalles sobre permiten nombres de base de datos, vea "Reglas de nomenclatura de objetos" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Restaurar una base de datos de usuario restaura una copia de seguridad completa y, a continuación, opcionalmente restaura una copia de seguridad diferencial para el dispositivo. Una restauración de una base de datos de usuario incluye la restauración de los usuarios de base de datos y roles de base de datos.  
  
 DESDE el disco = '\\\\*UNC_path*\\*backup_directory*'  
 La ruta de acceso de red y el directorio desde el que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaurará los archivos de copia de seguridad. Por ejemplo, desde el disco = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
 *backup_directory*  
 Especifica el nombre de un directorio que contiene la copia de seguridad completa o diferencial. Por ejemplo, puede realizar una operación RESTORE HEADERONLY en una copia de seguridad completa o diferencial.  
  
 *full_backup_directory*  
 Especifica el nombre de un directorio que contiene la copia de seguridad completa.  
  
 *differential_backup_directory*  
 Especifica el nombre del directorio que contiene la copia de seguridad diferencial.  
  
-   El directorio de copia de seguridad y la ruta de acceso debe existir y debe especificarse como una ruta de acceso UNC (convención) de nomenclatura de universal completo.  
  
-   La ruta de acceso al directorio de copia de seguridad no puede ser una ruta de acceso local y no puede ser una ubicación de la [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodos de dispositivo.  
  
-   La longitud máxima de la ruta de acceso UNC y el nombre del directorio de copia de seguridad es de 200 caracteres.  
  
-   El servidor o host debe especificarse como una dirección IP.  
  
 RESTORE HEADERONLY  
 Especifica que se devuelven únicamente la información de encabezado de copia de seguridad de base de datos de un usuario. Entre otros campos, el encabezado incluye la descripción de texto de la copia de seguridad y el nombre de la copia de seguridad. No es necesario el nombre de copia de seguridad ser el mismo que el nombre del directorio que almacena los archivos de copia de seguridad.  
  
 Resultados de RESTORE HEADERONLY se modelan después de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultados de RESTORE HEADERONLY. El resultado tiene más de 50 columnas, que no usa [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para obtener una descripción de las columnas de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resultados de RESTORE HEADERONLY, consulte [RESTORE HEADERONLY &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere la **CREATE ANY DATABASE** permiso.  
  
 Requiere una cuenta de Windows que tenga permiso para obtener acceso y leer desde el directorio de copia de seguridad. También debe almacenar el nombre de la cuenta de Windows y la contraseña en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
1.  Para comprobar las credenciales ya no existe, use aún [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  Para agregar o actualizar las credenciales, utilice [sp_pdw_add_network_credentials &#40; Almacenamiento de datos SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  Para quitar las credenciales de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_pdw_remove_network_credentials &#40; Almacenamiento de datos SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El comando Restaurar base de datos produce errores en las siguientes condiciones:  
  
-   El nombre de la base de datos para restaurar ya existe en el dispositivo de destino. Para evitar este problema, elija un nombre único de la base de datos o quitar la base de datos existente antes de ejecutar la restauración.  
  
-   Hay un conjunto de archivos de copia de seguridad en el directorio de copia de seguridad no válido.  
  
-   Los permisos de inicio de sesión no son suficientes para restaurar una base de datos.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]no tiene los permisos correctos a la ubicación de red donde se encuentran los archivos de copia de seguridad.  
  
-   La ubicación de red para el directorio de copia de seguridad no existe o no está disponible.  
  
-   No hay suficiente espacio en disco en los nodos de proceso o el nodo de Control. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]no se confirme que existe suficiente espacio en disco en el dispositivo antes de iniciar la restauración. Por lo tanto, es posible generar un error de falta de espacio en disco mientras se ejecuta la instrucción RESTORE DATABASE. Cuando se produce el suficiente espacio en disco, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] revierte la restauración.  
  
-   El dispositivo de destino al que se está restaurando la base de datos tiene menos nodos de proceso que el dispositivo de origen desde el que se copió la base de datos.  
  
-   Se intenta la restauración de base de datos desde dentro de una transacción.  
  
## <a name="general-remarks"></a>Notas generales  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]realiza un seguimiento del éxito de restauraciones de base de datos. Antes de restaurar una copia de seguridad diferencial de la base de datos, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] comprueba la restauración completa de la base de datos finalizó correctamente.  
  
 Después de una restauración, la base de datos de usuario tendrá nivel 120 de compatibilidad de base de datos. Esto es cierto para todas las bases de datos, independientemente de su nivel de compatibilidad original.  
  
 **Restaurar a un dispositivo con un gran número de nodos de proceso**  
Ejecutar [DBCC SHRINKLOG (almacenamiento de datos de SQL Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) después de restaurar una base de datos desde un dispositivo menor a mayor, ya que su redistribución, aumentará el registro de transacciones.  

Restaurar una copia de seguridad en un dispositivo con un gran número de nodos de proceso, aumenta el tamaño de base de datos asignado en proporción al número de nodos de cálculo.  
  
Por ejemplo, al restaurar un 60 GB base de datos desde un dispositivo de 2 nodos (30 GB por nodo) a un equipo de nodo de 6, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] crea una base de datos de 180 GB (6 nodos con 30 GB por nodo) en el dispositivo de 6 nodos. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]inicialmente se restaura la base de datos en 2 nodos para que coincida con la configuración de origen y, a continuación, redistribuye los datos a todos los nodos de 6.  
  
 Después de la redistribución cada nodo de proceso contiene menos datos reales y más espacio libre que cada nodo de ejecución en el dispositivo de origen más pequeño. Utilice el espacio adicional para agregar más datos a la base de datos. Si el tamaño de la base de datos restaurada es superior al necesario, puede usar [ALTER DATABASE &#40; Almacenamiento de datos en paralelo &#41; ](../../t-sql/statements/alter-database-parallel-data-warehouse.md) para reducir los tamaños de archivo de base de datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Para estas limitaciones y restricciones, el dispositivo de origen es el dispositivo desde el que se creó la copia de seguridad de base de datos y el dispositivo de destino es el dispositivo a la que se restaurará la base de datos.  
  
 Restaurar una base de datos no regenera automáticamente las estadísticas.  
  
 Instrucción solo Restaurar base de datos o base de datos de copia de seguridad puede ejecutarse en el dispositivo en un momento dado. Si varias instrucciones backup y restore se envían al mismo tiempo, el dispositivo se coloca en una cola y procesarlos uno a la vez.  
  
 Solo se puede restaurar una copia de seguridad de base de datos en un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo de destino que tenga el mismo número o más nodos de proceso que el dispositivo de origen. El dispositivo de destino no puede tener menos nodos de proceso que el dispositivo de origen.  
  
 No puede restaurar una copia de seguridad que se creó en un dispositivo que tenga un hardware con PDW de SQL Server 2012 a un dispositivo que tiene el hardware de SQL Server 2008 R2. Esto ocurre incluso si el dispositivo compró originalmente con el hardware de PDW de SQL Server 2008 R2 y ahora está ejecutando el software de PDW de SQL Server 2012.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo exclusivo en el objeto de base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-restore-examples"></a>A. Ejemplos de RESTORE simples  
 En el ejemplo siguiente se restaura una copia de seguridad completa para el `SalesInvoices2013` base de datos. Los archivos de copia de seguridad se almacenan en la \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full directory. La base de datos SalesInvoices2013 no debe existir ya en el dispositivo de destino o este comando producirá un error.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. Restaurar una copia de seguridad completa y diferencial  
 En el ejemplo siguiente se restaura una completa y, a continuación, una copia de seguridad diferencial para la base de datos SalesInvoices2013  
  
 La copia de seguridad completa de la base de datos se restaura desde la copia de seguridad que se almacena en el '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full' directorio. Si la restauración se completa correctamente, se restaura la copia de seguridad diferencial para la base de datos de SalesInvoices2013.  La copia de seguridad diferencial se almacena en el '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff' directorio.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Restaurar el encabezado de copia de seguridad  
 Este ejemplo restaura la información de encabezado de copia de seguridad de base de datos '\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'. Los resultados del comando en una fila de la información de la copia de seguridad de Invoices2013Full.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 Puede usar la información de encabezado para comprobar el contenido de una copia de seguridad, o para asegurarse de que el dispositivo de restauración de destino es compatible con el dispositivo de copia de seguridad de origen antes de intentar restaurar la copia de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [Base de datos de copia de seguridad &#40; Almacenamiento de datos en paralelo &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  

