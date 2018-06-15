---
title: RESTORE DATABASE (Almacenamiento de datos paralelos) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ed7e6aeb0630a20ee39d512fc17dfe24040737f2
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33702519"
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTORE DATABASE (Almacenamiento de datos paralelos)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Restaura una base de datos de usuario de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] desde una copia de seguridad de base de datos a un dispositivo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. La base de datos se restaura desde una copia de seguridad que se creó anteriormente con el comando [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][BACKUP DATABASE &#40;Almacenamiento de datos paralelos&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md). Use las operaciones de copia de seguridad y de restauración para crear un plan de recuperación ante desastres o para mover bases de datos de un dispositivo a otro.  
  
> [!NOTE]  
>  Restaurar la base de datos maestra conlleva restaurar la información de inicio de sesión del dispositivo. Para restaurar la base de datos maestra, use la página [Restaurar la base de datos maestra &#40;Transact-SQL&#41; ](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) de la herramienta **Configuration Manager**. Un administrador con acceso al nodo de control puede realizar esta operación.  
  
 Para más información sobre las copias de seguridad de bases de datos de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], vea "Copia de seguridad y restauración" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 RESTORE DATABASE *database_name*  
 Especifica que una base de datos de usuario se debe restaurar a una base de datos denominada *database_name*. La base de datos restaurada puede tener un nombre diferente de la base de datos de origen de la que se ha hecho la copia de seguridad. *database_name* no puede existir como una base de datos en el dispositivo de destino. Para más información sobre los nombres de base de datos permitidos, vea "Normas de nomenclatura de objetos" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Cuando se restaura una base de datos de usuario, se restaura una copia de seguridad completa de la base de datos y, después, se restaura (opcionalmente) una copia de seguridad diferencial en el dispositivo. La restauración de una base de datos de usuario conlleva restaurar los usuarios de base de datos y los roles de base de datos.  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 Ruta de acceso de red y directorio desde los que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaurará los archivos de copia de seguridad. Por ejemplo, FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
 *backup_directory*  
 Especifica el nombre de un directorio que contiene la copia de seguridad completa o diferencial. Por ejemplo, puede realizar una operación RESTORE HEADERONLY en una copia de seguridad completa o diferencial.  
  
 *full_backup_directory*  
 Especifica el nombre de un directorio que contiene la copia de seguridad completa.  
  
 *differential_backup_directory*  
 Especifica el nombre de un directorio que contiene la copia de seguridad diferencial.  
  
-   La ruta de acceso y el directorio de copia de seguridad ya deben existir y se debe especificar como una ruta de acceso de convención de nomenclatura universal (UNC) completa.  
  
-   La ruta de acceso al directorio de copia de seguridad no puede ser una ruta de acceso local y no puede ser una ubicación en ninguno de los nodos del dispositivo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
-   La longitud máxima de la ruta de acceso UNC y el nombre del directorio de copia de seguridad es de 200 caracteres.  
  
-   El servidor o host se debe especificar como una dirección IP.  
  
 RESTORE HEADERONLY  
 Especifica que se devuelve únicamente la información de encabezado de una copia de seguridad de base de datos de usuario. Entre otros campos, el encabezado incluye el nombre y la descripción de texto de la copia de seguridad. El nombre de copia de seguridad no tiene que ser el mismo que el nombre del directorio donde se almacenan los archivos de copia de seguridad.  
  
 El formato de los resultados de RESTORE HEADERONLY se toma de los resultados de RESTORE HEADERONLY de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El resultado tiene más de 50 columnas, que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no usa en su totalidad. Para obtener una descripción de las columnas de los resultados de RESTORE HEADERONLY de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **CREATE ANY DATABASE**.  
  
 Requiere una cuenta de Windows que tenga permiso de acceso y lectura en el directorio de copia de seguridad. También se debe almacenar el nombre de la cuenta de Windows y la contraseña en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
1.  Para confirmar que las credenciales ya están ahí, use [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  Para agregar o actualizar las credenciales, vea [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  Para quitar las credenciales de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El comando RESTORE DATABASE genera errores en las siguientes circunstancias:  
  
-   El nombre de la base de datos que se va a restaurar ya existe en el dispositivo de destino. Para evitarlo, elija un nombre de base de datos único o quite la base de datos existente antes de proceder a realizar la restauración.  
  
-   Hay un conjunto de archivos de copia de seguridad no válido en el directorio de copia de seguridad.  
  
-   Los permisos de inicio de sesión no son suficientes para restaurar la base de datos.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no tiene los permisos correctos en la ubicación de red donde van a estar los archivos de copia de seguridad.  
  
-   La ubicación de red del directorio de copia de seguridad no existe o no está disponible.  
  
-   No hay suficiente espacio en disco en los nodos de ejecución o de control. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no confirma que hay suficiente espacio en disco en el dispositivo antes de iniciar la restauración. Por lo tanto, es posible que surja un error de espacio en disco agotado mientras se ejecuta la instrucción RESTORE DATABASE. Cuando se produce un error de espacio en disco insuficiente, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] revierte la restauración.  
  
-   El dispositivo de destino en el que se está restaurando la base de datos tiene menos nodos de ejecución que el dispositivo de origen desde el que se hizo la copia de seguridad de la base de datos.  
  
-   La restauración de base de datos se intenta realizar desde dentro de una transacción.  
  
## <a name="general-remarks"></a>Notas generales  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] realiza un seguimiento para saber qué restauraciones de base de datos se realizan correctamente. Antes de restaurar una copia de seguridad diferencial de la base de datos, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] comprueba si la restauración de base de datos completa finalizó correctamente.  
  
 Después de una restauración, la base de datos de usuario tendrá nivel 120 de compatibilidad de base de datos. Esto sucede con todas las bases de datos, independientemente de su nivel de compatibilidad original.  
  
 **Restaurar a un dispositivo con más nodos de ejecución**  
Ejecute [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) después de restaurar una base de datos desde un dispositivo más pequeño a uno más grande, ya que la redistribución aumentará el registro de transacciones.  

Restaurar una copia de seguridad en un dispositivo con un gran número de nodos de ejecución aumenta el tamaño de base de datos asignado en proporción al número de nodos de ejecución.  
  
Por ejemplo, al restaurar una base de datos de 60 GB desde un dispositivo con 2 nodos (30 GB por nodo) a un equipo con 6 nodos, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] crea una base de datos de 180 GB (6 nodos con 30 GB cada uno) en el dispositivo de 6 nodos. En principio, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restaura la base de datos a 2 nodos para que coincida con la configuración de origen y, seguidamente, redistribuye los datos a los 6 nodos.  
  
 Después de la redistribución, cada nodo de ejecución contendrá menos datos reales y más espacio libre que cada nodo de ejecución en el dispositivo de origen (más pequeño). Use el espacio extra para agregar más datos a la base de datos. Si el tamaño de la base de datos restaurada es superior al necesario, puede usar [ALTER DATABASE &#40;Almacenamiento de datos paralelos&#41; ](../../t-sql/statements/alter-database-parallel-data-warehouse.md) para reducir el tamaño de los archivos de la base de datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 En estas limitaciones y restricciones, el dispositivo de origen es el dispositivo desde el que se creó la copia de seguridad de la base de datos y el dispositivo de destino, el dispositivo en el que se va a restaurar esa base de datos.  
  
 Restaurar una base de datos no vuelve a generar automáticamente las estadísticas.  
  
 En el dispositivo solo se puede ejecutar una instrucción RESTORE DATABASE o BACKUP DATABASE en un momento dado. Si se envían varias instrucciones BACKUP y RESTORE al mismo tiempo, el dispositivo las pone en cola y las procesa una a una.  
  
 Solo se puede restaurar una copia de seguridad de base de datos en un dispositivo de destino de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] que tenga el mismo número o más nodos de ejecución que el dispositivo de origen. El dispositivo de destino no puede tener menos nodos de ejecución que el de origen.  
  
 Una copia de seguridad creada en un dispositivo con hardware de PDW de SQL Server 2012 no se puede restaurar en un dispositivo que tenga hardware de SQL Server 2008 R2. Esto es así incluso si el dispositivo se adquirió originalmente con el hardware de PDW de SQL Server 2008 R2 y ahora ejecuta el hardware de PDW de SQL Server 2012.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo exclusivo en el objeto DATABASE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-restore-examples"></a>A. Ejemplos sencillos de RESTORE  
 En el siguiente ejemplo se restaura una copia de seguridad completa en la base de datos `SalesInvoices2013`. Los archivos de copia de seguridad se almacenan en el directorio \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full. La base de datos SalesInvoices2013 no debe existir ya en el dispositivo de destino o, de lo contrario, este comando producirá un error.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. Restaurar una copia de seguridad completa y diferencial  
 En el siguiente ejemplo se restaura una copia de seguridad completa y, luego, una diferencial en la base de datos SalesInvoices2013.  
  
 La copia de seguridad completa de la base de datos se restaura a partir de la copia de seguridad que se almacena en el directorio "\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full". Si la restauración se completa correctamente, la copia de seguridad diferencial se restaura en la base de datos SalesInvoices2013.  La copia de seguridad diferencial se almacena en el directorio "\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff".  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Restaurar el encabezado de copia de seguridad  
 En este ejemplo se restaura la información de encabezado de la copia de seguridad de base de datos "\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full". El comando da como resultado una fila de información relativa a la copia de seguridad de Invoices2013Full.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 Esta información de encabezado puede servir para comprobar el contenido de una copia de seguridad o para asegurarse de que el dispositivo de restauración de destino es compatible con el dispositivo de copia de seguridad de origen antes de intentar restaurar la copia de seguridad.  
  
## <a name="see-also"></a>Ver también  
 [BACKUP DATABASE &#40;Almacenamiento de datos paralelos&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
