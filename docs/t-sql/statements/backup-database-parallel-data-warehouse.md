---
title: BACKUP DATABASE (Almacenamiento de datos paralelos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f37da7b17e77199f41c4c0f2fd3f9959958fcf8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="backup-database-parallel-data-warehouse"></a>BACKUP DATABASE (Almacenamiento de datos paralelos)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Crea una copia de seguridad de una base de datos de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] y la almacena fuera del dispositivo en una ubicación de red especificada por el usuario. Use esta instrucción con [RESTORE DATABASE &#40;Almacenamiento de datos paralelos&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md) para la recuperación ante desastres, o bien para copiar una base de datos de un dispositivo a otro.  
  
 **Antes de comenzar**, vea "Adquirir y configurar un servidor de copia de seguridad" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] hay dos tipos de copias de seguridad. Una *copia de seguridad completa de base de datos* es una copia de seguridad de una base de datos de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] completa. Una *copia de seguridad diferencial* solo incluye los cambios realizados desde la última copia de seguridad completa de base de datos. Una copia de seguridad de una base de datos de usuario incluye usuarios de base de datos y roles de base de datos. Una copia de seguridad de la base de datos maestra incluye los inicios de sesión.  
  
 Para más información sobre las copias de seguridad de bases de datos de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], vea "Copia de seguridad y restauración" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos en la que se va a crear una copia de seguridad. La base de datos puede ser la base de datos maestra o una base de datos de usuario.  
  
 TO DISK = '\\\\*UNC_path*\\*backup_directory*'  
 La ruta de acceso de red y el directorio en el que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] escribirá los archivos de copia de seguridad. Por ejemplo, "\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup".  
  
-   La ruta de acceso al nombre del directorio de copia de seguridad ya debe existir y se debe especificar como una ruta de acceso de convención de nomenclatura universal (UNC) completa.  
  
-   El directorio de copia de seguridad, *directorio_de_copia_de_seguridad*, no debe existir antes de ejecutar el comando de copia de seguridad. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] creará el directorio de copia de seguridad.  
  
-   La ruta de acceso al directorio de copia de seguridad no puede ser una ruta de acceso local y no puede ser una ubicación en ninguno de los nodos del dispositivo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
-   La longitud máxima de la ruta de acceso UNC y el nombre del directorio de copia de seguridad es de 200 caracteres.  
  
-   El servidor o host se debe especificar como una dirección IP.  No se puede especificar como el nombre de host o servidor.  
  
 DESCRIPTION = **"***texto***"**  
 Especifica una descripción textual de la copia de seguridad. La longitud máxima del texto es 255 caracteres.  
  
 La descripción se almacena en los metadatos y se mostrará cuando se restaure el encabezado de copia de seguridad con RESTORE HEADERONLY.  
  
 NAME = **'***backup _name***'**  
 Especifica el nombre de la copia de seguridad. El nombre de la copia de seguridad puede ser distinto del nombre de la base de datos.  
  
-   Los nombres pueden tener un máximo de 128 caracteres.  
  
-   No puede incluir una ruta de acceso.  
  
-   Debe comenzar con una letra o un carácter numérico, o bien un carácter de subrayado (_). Los caracteres especiales permitidos son el carácter de subrayado (\_), guión (-) o espacio ( ). Los nombres de copia de seguridad no pueden terminar con un carácter de espacio.  
  
-   Se producirá un error en la instrucción si *backup_name* ya existe en la ubicación especificada.  
  
 Este nombre se almacena en los metadatos y se mostrará cuando se restaure el encabezado de copia de seguridad con RESTORE HEADERONLY.  
  
 DIFFERENTIAL  
 Especifica que se realice una copia de seguridad diferencial de una base de datos de usuario. Si se omite, el valor predeterminado es una copia de seguridad completa de base de datos. No es necesario que el nombre de la copia de seguridad diferencial coincida con el nombre de la copia de seguridad completa. Para realizar el seguimiento de la copia diferencial y su copia de seguridad completa correspondiente, considere la posibilidad de usar el mismo nombre con "completa" o "diferencial" anexado.  
  
 Por ejemplo:  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **BACKUP DATABASE** o la pertenencia al rol fijo de base de datos **db_backupoperator**. Un usuario normal que se haya agregado al rol fijo de base de datos **db_backupoperator** no puede hacer una copia de seguridad de la base de datos maestra. Solo **sa**, el administrador del tejido o los miembros del rol fijo de servidor **sysadmin** pueden hacer una copia de seguridad de la base de datos maestra.  
  
 Requiere una cuenta de Windows que tenga permiso para obtener acceso, crear y escribir en el directorio de copia de seguridad. También se debe almacenar el nombre de la cuenta de Windows y la contraseña en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para agregar estas credenciales de red a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el procedimiento almacenado [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
 Para obtener más información sobre cómo administrar las credenciales en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], vea la sección [Seguridad](#Security).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Errores de BACKUP DATABASE en las siguientes circunstancias:  
  
-   Los permisos de usuario no son suficientes para realizar una copia de seguridad.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no tiene los permisos correctos a la ubicación de red donde se almacenará la copia de seguridad.  
  
-   La base de datos no existe.  
  
-   El directorio de destino ya existe en el recurso compartido de red.  
  
-   El recurso compartido de red de destino no está disponible.  
  
-   El recurso compartido de red de destino no tiene suficiente espacio para la copia de seguridad. El comando BACKUP DATABASE no confirma que existe suficiente espacio en disco antes de iniciar la copia de seguridad, lo que permite generar un error de espacio en disco insuficiente mientras se ejecuta BACKUP DATABASE. Cuando se produce el error de espacio en disco insuficiente, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] revierte el comando BACKUP DATABASE. Para reducir el tamaño de la base de datos, ejecute [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md).  
  
-   Se intenta iniciar una copia de seguridad dentro de una transacción.  
  
## <a name="general-remarks"></a>Notas generales  
 Antes de realizar una copia de seguridad de base de datos, use [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para reducir el tamaño de la base de datos. 
 
 Una copia de seguridad de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] se almacena como un conjunto de varios archivos en el mismo directorio.  
  
 Una copia de seguridad diferencial normalmente tarda menos tiempo que una copia de seguridad completa y se puede realizar con más frecuencia. Cuando varias copias de seguridad diferenciales se basan en la misma copia de seguridad completa, cada copia diferencial incluye todos los cambios de la copia de seguridad diferencial anterior.  
  
 Si se cancela un comando BACKUP, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] quitará el directorio de destino y todos los archivos creados para la copia de seguridad. Si [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] pierde conectividad de red para el recurso compartido, la reversión no se puede completar.  
  
 Las copias de seguridad completas y diferenciales se almacenan en directorios independientes. No se aplican las convenciones de nomenclatura para especificar que una copia de seguridad completa y una copia de seguridad diferencial forman un conjunto. Puede realizar el seguimiento de esto a través de sus propias convenciones de nomenclatura. Como alternativa, puede controlar esto mediante la opción WITH DESCRIPTION para agregar una descripción y, después, mediante la instrucción RESTORE HEADERONLY para recuperar la descripción.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede realizar una copia de seguridad diferencial de la base de datos maestra. Solo se admiten las copias de seguridad completas de la base de datos maestra.  
  
 Los archivos de copia de seguridad se almacenan en un formato adecuado únicamente para restaurar la copia de seguridad en un dispositivo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] mediante la instrucción [RESTORE DATABASE &#40;Almacenamiento de datos paralelos&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md).  
  
 No se puede usar la copia de seguridad con la instrucción BACKUP DATABASE para transferir datos o información del usuario a bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de SMP. Para esa funcionalidad, se puede usar la característica de copia de la tabla remota. Para más información, vea "Copia de la tabla remota" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] se usa la tecnología de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para realizar copias de seguridad y restaurar bases de datos. Las opciones de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están preconfiguradas para usar la compresión de copia de seguridad. No se pueden establecer opciones de copia de seguridad como la compresión, suma de comprobación, tamaño de bloque y recuento de búferes.  
  
 Solo se puede ejecutar una copia de seguridad o restauración de base de datos en el dispositivo en un momento dado. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] pondrá en cola los comandos de copia de seguridad o restauración hasta que se haya completado el comando actual de copia de seguridad o restauración.  
  
 El dispositivo de destino para restaurar la copia de seguridad debe tener al menos tantos nodos de ejecución como el dispositivo de origen. El destino puede tener más nodos de ejecución que el dispositivo de origen, pero no menos.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no realiza el seguimiento de la ubicación y los nombres de las copias de seguridad, ya que las copias de seguridad se almacenan fuera del dispositivo.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] realiza el seguimiento del éxito o el fracaso de las copias de seguridad de base de datos.  
  
 Solo se permite una copia de seguridad diferencial si la última copia de seguridad completa se realizó correctamente. Por ejemplo, suponga que el lunes crea una copia de seguridad completa de la base de datos de ventas y la copia de seguridad finaliza correctamente. Después, el martes crea una copia de seguridad completa de la base de datos de ventas y se produce un error. Después de este error, no puede crear una copia de seguridad diferencial basada en la copia de seguridad completa del lunes. Primero debe crear una copia de seguridad completa correcta antes de crear una copia de seguridad diferencial.  
  
## <a name="metadata"></a>Metadatos  
 Estas vistas de administración dinámicas contienen información sobre todas operaciones de copia de seguridad, restauración y carga. La información se conserva entre reinicios del sistema.  
  
-   [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>Rendimiento  
 Para realizar una copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] primero crea una copia de seguridad de los metadatos y, después, realiza una copia de seguridad paralela de los datos de base de datos almacenados en los nodos de ejecución. Los datos se copian directamente desde cada nodo de ejecución al directorio de copia de seguridad. Para obtener el mejor rendimiento para mover los datos de los nodos de ejecución al directorio de copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] controla el número de nodos de ejecución en los que se copian datos al mismo tiempo.  
  
## <a name="locking"></a>Bloqueo  
 Toma un bloqueo ExclusiveUpdate en el objeto de base de datos.  
  
##  <a name="Security"></a> Seguridad  
 Las copias de seguridad de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] no se almacenan en el dispositivo. Por tanto, el equipo de TI es responsable de administrar todos los aspectos de la seguridad de las copias de seguridad. Por ejemplo, esto incluye la administración de la seguridad de los datos de copia de seguridad, la del servidor que se usa para almacenar las copias de seguridad y la de la infraestructura de red que conecta el servidor de copia de seguridad con el dispositivo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 **Administrar las credenciales de red**  
  
 El acceso de red al directorio de copia de seguridad se basa en la seguridad del uso compartido de archivos de Windows estándar. Antes de realizar una copia de seguridad, debe crear o designar una cuenta de Windows que se usó para la autenticación de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] en el directorio de copia de seguridad. Esta cuenta de Windows debe tener permiso para obtener acceso, crear y escribir en el directorio de copia de seguridad.  
  
> [!IMPORTANT]  
>  Para reducir los riesgos de seguridad con los datos, se recomienda designar una cuenta de Windows exclusivamente para realizar las operaciones de copia de seguridad y restauración. Permita que esta cuenta tenga permisos para la ubicación de la copia de seguridad y ningún otro lugar más.  
  
 Debe almacenar el nombre de usuario y la contraseña en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] mediante la ejecución del procedimiento almacenado [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md). [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] usa el Administrador de credenciales de Windows para almacenar y cifrar los nombres de usuario y las contraseñas en el nodo de control y los nodos de ejecución. No se realiza una copia de seguridad de las credenciales con el comando BACKUP DATABASE.  
  
 Para quitar las credenciales de red de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], vea [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 Para enumerar todas las credenciales de red almacenadas en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use la vista de administración dinámica [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Agregar credenciales de red para la ubicación de copia de seguridad  
 Para crear una copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] debe tener permiso de lectura/escritura en el directorio de copia de seguridad. En el ejemplo siguiente se muestra cómo agregar las credenciales de un usuario. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] almacenará estas credenciales y las usará para las operaciones de copias de seguridad y restauración.  
  
> [!IMPORTANT]  
>  Por motivos de seguridad, se recomienda crear una cuenta de dominio exclusivamente para realizar copias de seguridad.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. Quitar credenciales de red para la ubicación de copia de seguridad  
 En el ejemplo siguiente se muestra cómo quitar las credenciales de un usuario de dominio de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Creación de una copia de seguridad completa de una base de datos de usuario  
 En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos de usuario Invoices. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] creará el directorio Invoices2013 y guardará los archivos de copia de seguridad en el directorio \\\10.192.63.147\backups\yearly\Invoices2013Full.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Crear una copia de seguridad diferencial de una base de datos de usuario  
 En el ejemplo siguiente se crea una copia de seguridad diferencial, que incluye todos los cambios realizados desde la última copia de seguridad completa de la base de datos Invoices. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] creará el directorio \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff en el que almacenará los archivos. La descripción "Invoices 2013 differential backup" (Copia de seguridad diferencial de Invoices 2013) se almacenará con la información de encabezado de la copia de seguridad.  
  
 La copia de seguridad diferencial solo se ejecutará correctamente si la última copia de seguridad completa de Invoices se completó correctamente.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Crear una copia de seguridad completa de la base de datos maestra  
 En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos maestra y se almacena en el directorio "\\\10.192.63.147\backups\2013\daily\20130722\master".  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Crear una copia de seguridad de la información de inicio de sesión del dispositivo.  
 En la base de datos maestra se almacena la información de inicio de sesión del dispositivo. Para realizar una copia de seguridad de la información de inicio de sesión del dispositivo es necesario realizar una copia de seguridad de la base de datos maestra.  
  
 En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos maestra.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Ver también  
 [RESTORE DATABASE &#40;Almacenamiento de datos paralelos&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
