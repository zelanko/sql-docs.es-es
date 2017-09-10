---
title: Base de datos de copia de seguridad (almacenamiento de datos en paralelo) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fb36fd89c02ff9ddd5bc33825a387b53ab6e174
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="backup-database-parallel-data-warehouse"></a>Base de datos de copia de seguridad (almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Crea una copia de seguridad de un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] la base de datos y almacena la copia de seguridad desactivar el dispositivo en una ubicación de red especificada por el usuario. Use esta instrucción con [Restaurar base de datos &#40; Almacenamiento de datos en paralelo &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) para recuperación ante desastres, o para copiar una base de datos de un dispositivo a otro.  
  
 **Antes de comenzar**, vea "Adquirir y configurar un servidor de copia de seguridad" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Hay dos tipos de copias de seguridad en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. A *copia de seguridad de base de datos completa* es una copia de seguridad de toda una [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] base de datos. A *copia de seguridad diferencial* solo incluye los cambios realizados desde la última copia de seguridad completa. Una copia de seguridad de una base de datos de usuario incluye usuarios de base de datos y roles de base de datos. Una copia de seguridad de la base de datos maestra incluye inicios de sesión.  
  
 Para obtener más información acerca de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] copias de seguridad de base de datos, vea "Copia de seguridad y restauración" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 El nombre de la base de datos que se va a crear una copia de seguridad. La base de datos puede ser la base de datos maestra o una base de datos de usuario.  
  
 EN el disco = '\\\\*UNC_path*\\*backup_directory*'  
 La ruta de acceso de red y el directorio en el que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] escribirá los archivos de copia de seguridad. Por ejemplo, '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
-   La ruta de acceso para el nombre del directorio de copia de seguridad debe existir y debe especificarse como una ruta de acceso UNC (convención) de nomenclatura de universal completo.  
  
-   El directorio de copia de seguridad, *backup_directory*, no debe existir antes de ejecutar el comando de copia de seguridad. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]se creará el directorio de copia de seguridad.  
  
-   La ruta de acceso al directorio de copia de seguridad no puede ser una ruta de acceso local y no puede ser una ubicación de la [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nodos de dispositivo.  
  
-   La longitud máxima de la ruta de acceso UNC y el nombre del directorio de copia de seguridad es de 200 caracteres.  
  
-   El servidor o host debe especificarse como una dirección IP.  No se puede especificarla como el nombre de host o servidor.  
  
 DESCRIPCIÓN = **'***texto***'**  
 Especifica una descripción textual de la copia de seguridad. La longitud máxima del texto es de 255 caracteres.  
  
 La descripción se almacena en los metadatos y se mostrará cuando el encabezado de copia de seguridad se restaura con RESTORE HEADERONLY.  
  
 NOMBRE = **'***_name copia de seguridad***'**  
 Especifica el nombre de la copia de seguridad. El nombre de la copia de seguridad puede ser distinto del nombre de la base de datos.  
  
-   Los nombres pueden tener un máximo de 128 caracteres.  
  
-   No puede incluir una ruta de acceso.  
  
-   Debe comenzar con una letra o un número de caracteres o un carácter de subrayado (_). Los caracteres especiales permitidos son el carácter de subrayado (\_), guión (-) o espacio (). Nombres de copia de seguridad no pueden terminar con un carácter de espacio.  
  
-   La instrucción se producirá un error si *nombre_copiaSeguridad* ya existe en la ubicación especificada.  
  
 Este nombre se almacena en los metadatos y se mostrará cuando el encabezado de copia de seguridad se restaura con RESTORE HEADERONLY.  
  
 DIFFERENTIAL  
 Especifica que se realice una copia de seguridad diferencial de una base de datos de usuario. Si se omite, el valor predeterminado es una copia de seguridad completa de la base de datos. No es necesario el nombre de la copia de seguridad diferencial para que coincida con el nombre de la copia de seguridad completa. Para mantener un seguimiento de la copia diferencial y su copia de seguridad completa correspondiente, considere la posibilidad de con el mismo nombre con 'total' o 'diferencias' anexado.  
  
 Por ejemplo:  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Permissions  
 Requiere la **base de datos de copia de seguridad** permiso o la pertenencia a la **db_backupoperator** rol fijo de base de datos. La base de datos maestra no puede hacerse una pero si un usuario normal que se agregó a la **db_backupoperator** rol fijo de base de datos. La base de datos maestra solo puede estar respaldada por **sa**, el administrador del tejido o los miembros de la **sysadmin** rol fijo de servidor.  
  
 Requiere una cuenta de Windows que tenga permiso para tener acceso, crear y escribir en el directorio de copia de seguridad. También debe almacenar el nombre de la cuenta de Windows y la contraseña en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Para agregar estas credenciales de red a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el [sp_pdw_add_network_credentials &#40; Almacenamiento de datos SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento almacenado.  
  
 Para obtener más información acerca de cómo administrar las credenciales en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], consulte el [seguridad](#Security) sección.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Errores de base de datos de copia de seguridad en las siguientes condiciones:  
  
-   Permisos de usuario no son suficientes para realizar una copia de seguridad.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]no tiene los permisos correctos a la ubicación de red donde se almacenará la copia de seguridad.  
  
-   La base de datos no existe.  
  
-   El directorio de destino ya existe en el recurso compartido de red.  
  
-   El recurso compartido de red de destino no está disponible.  
  
-   El recurso compartido de red de destino no tiene suficiente espacio para la copia de seguridad. El comando de base de datos de copia de seguridad no confirma que existe suficiente espacio en disco antes de iniciar la copia de seguridad, lo que permite generar un error de falta de espacio en disco mientras se ejecuta la copia de seguridad de la base de datos. Cuando se produce el suficiente espacio en disco, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] revierte el comando de base de datos de copia de seguridad. Para reducir el tamaño de la base de datos, ejecutar [DBCC SHRINKLOG (almacenamiento de datos de SQL Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   Intente iniciar una copia de seguridad dentro de una transacción.  
  
## <a name="general-remarks"></a>Notas generales  
 Antes de realizar una copia de seguridad de base de datos, utilice [DBCC SHRINKLOG (almacenamiento de datos de SQL Azure)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) para reducir el tamaño de la base de datos. 
 
 A [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] copia de seguridad se almacena como un conjunto de varios archivos en el mismo directorio.  
  
 Una copia de seguridad diferencial normalmente tarda menos tiempo que una copia de seguridad completa y se puede realizar con más frecuencia. Cuando varias copias de seguridad diferenciales se basan en la misma copia de seguridad completa, cada diferencial incluye todos los cambios en la copia de seguridad diferencial anterior.  
  
 Si se cancela un comando de copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] quitará el directorio de destino y todos los archivos creados para la copia de seguridad. Si [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] pierde conectividad de red para el recurso compartido, no se puede completar la reversión.  
  
 Copias de seguridad completas y diferenciales se almacenan en directorios independientes. No se aplican las convenciones de nomenclatura para especificar que una copia de seguridad completa y una copia de seguridad diferencial forman un conjunto. Puede realizar un seguimiento de esto a través de sus propias convenciones de nomenclatura. Como alternativa, puede controlar esto mediante la opción con la descripción para agregar una descripción y, a continuación, mediante la instrucción RESTORE HEADERONLY para recuperar la descripción.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede realizar una copia de seguridad diferencial de la base de datos maestra. Se admiten solo copias de seguridad completas de la base de datos maestra.  
  
 Los archivos de copia de seguridad se almacenan en un formato adecuado sólo para restaurar la copia de seguridad para un [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo usando la [Restaurar base de datos &#40; Almacenamiento de datos en paralelo &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) instrucción.  
  
 No se puede usar la copia de seguridad con la instrucción BACKUP DATABASE para transferir datos o información del usuario a SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos. Para que la funcionalidad, puede usar la característica de copia de la tabla remota. Para obtener más información, vea "Copia de la tabla remota" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnología de copia de seguridad y restaurar bases de datos de copia de seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Opciones de copia de seguridad están preconfigurados para utilizar la compresión de copia de seguridad. No se puede establecer opciones de copia de seguridad como la compresión, suma de comprobación, tamaño de bloque y recuento de búfer.  
  
 Solo una copia de seguridad o restauración, se puede ejecutar en el dispositivo en un momento dado. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]se pondrán en cola comandos de copia de seguridad o restauración hasta que la copia de seguridad actual o se ha completado el comando de restauración.  
  
 El dispositivo de destino para restaurar la copia de seguridad debe tener al menos tantos nodos de proceso que el dispositivo de origen. El destino puede tener más nodos de proceso que el dispositivo de origen, pero no puede tener menos nodos de cálculo.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]no realizar un seguimiento de la ubicación y los nombres de las copias de seguridad, ya que se almacenan las copias de seguridad desactivado el dispositivo.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]realiza un seguimiento el éxito o fracaso de las copias de seguridad de base de datos.  
  
 Solo se permite una copia de seguridad diferencial si la última copia de seguridad se completó correctamente. Por ejemplo, suponga que el lunes crear una copia de seguridad completa de la base de datos de ventas y la copia de seguridad ha finalizado correctamente. A continuación, el martes se crea una copia de seguridad completa de la base de datos de ventas y se produce un error. Después de este error, a continuación, no se puede crear una copia de seguridad diferencial en función de copia de seguridad completa del lunes. En primer lugar debe crear una copia de seguridad completa antes de crear una copia de seguridad diferencial.  
  
## <a name="metadata"></a>Metadatos  
 Estas vistas de administración dinámica contienen información acerca de todas las copias de seguridad, restauración y operaciones de carga. La información se conserva entre reinicios del sistema.  
  
-   [Sys.pdw_loader_backup_runs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [Sys.pdw_loader_backup_run_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [Sys.pdw_loader_run_stages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>Rendimiento  
 Para realizar una copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] primera copia de los metadatos y, a continuación, realiza una copia de seguridad paralela de los datos de la base de datos almacenados en los nodos de proceso. Datos se copian directamente desde los nodos de cada proceso en el directorio de copia de seguridad. Para obtener el mejor rendimiento para mover los datos de los nodos de proceso en el directorio de copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] controla el número de nodos de proceso que se va a copiar datos al mismo tiempo.  
  
## <a name="locking"></a>Bloqueo  
 Impone un bloqueo de ExclusiveUpdate en el objeto de base de datos.  
  
##  <a name="Security"></a> Seguridad  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]las copias de seguridad no se almacenan en el dispositivo. Por lo tanto, su equipo de TI es responsable de administrar todos los aspectos de la seguridad de copia de seguridad. Por ejemplo, esto incluye la administración de la seguridad de los datos de copia de seguridad, la seguridad del servidor utilizado para almacenar las copias de seguridad y la seguridad de la infraestructura de red que conecta el servidor de copia de seguridad para el [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo.  
  
 **Administrar credenciales de red**  
  
 Acceso de red al directorio de copia de seguridad se basa en el uso compartido seguridad de archivos de Windows estándar. Antes de realizar una copia de seguridad, debe crear o designar una cuenta de Windows que se utilizará para la autenticación de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] en el directorio de copia de seguridad. Esta cuenta de windows debe tener permiso para tener acceso, crear y escribir en el directorio de copia de seguridad.  
  
> [!IMPORTANT]  
>  Para reducir los riesgos de seguridad con los datos, se recomienda que designa una cuenta de Windows solamente con el fin de realizar la copia de seguridad y las operaciones de restauración. Permitir que esta cuenta tenga permisos para la ubicación de copia de seguridad y ningún otro lugar.  
  
 Debe almacenar el nombre de usuario y la contraseña en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ejecutando el [sp_pdw_add_network_credentials &#40; Almacenamiento de datos SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento almacenado. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]utiliza el Administrador de credenciales de Windows para almacenar y cifrar los nombres de usuario y contraseñas en el nodo de Control y los nodos de proceso. Las credenciales no se copiarán con el comando de base de datos de copia de seguridad.  
  
 Para quitar las credenciales de red de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], consulte [sp_pdw_remove_network_credentials &#40; Almacenamiento de datos SQL &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 Para enumerar todas las credenciales de red almacenado en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) vista de administración dinámica.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Agregar credenciales de red para la ubicación de copia de seguridad  
 Para crear una copia de seguridad, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] debe tener permiso de lectura/escritura en el directorio de copia de seguridad. En el ejemplo siguiente se muestra cómo agregar las credenciales de un usuario. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]almacenar estas credenciales y utilizarlas para copia de seguridad y las operaciones de restauración.  
  
> [!IMPORTANT]  
>  Por motivos de seguridad, se recomienda crear una cuenta de dominio únicamente con el fin de realizar copias de seguridad.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. Quitar las credenciales de red para la ubicación de copia de seguridad  
 En el ejemplo siguiente se muestra cómo quitar las credenciales de un usuario de dominio de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Crear una copia de seguridad completa de una base de datos de usuario  
 En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos de usuario de facturas. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]se creará el directorio Invoices2013 y guardará los archivos de copia de seguridad para el \\\10.192.63.147\backups\yearly\Invoices2013Full directory.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Crear una copia de seguridad diferencial de una base de datos de usuario  
 En el ejemplo siguiente se crea una copia de seguridad diferencial, que incluye todos los cambios realizados desde la última copia de seguridad completa de la base de datos de facturas. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]se creará el \\directorio \xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff en el que almacenará los archivos. La descripción 'copia de seguridad diferencial de facturas 2013' se almacenarán con la información de encabezado de la copia de seguridad.  
  
 La copia de seguridad diferencial solo se ejecutará correctamente si la última copia de seguridad completa de facturas se completó correctamente.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Crear una copia de seguridad completa de la base de datos maestra  
 En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos maestra y lo almacena en el directorio '\\\10.192.63.147\backups\2013\daily\20130722\master'.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Crear una copia de seguridad de la información de inicio de sesión del dispositivo.  
 La base de datos almacena la información de inicio de sesión del equipo. Copias de seguridad de la información de inicio de sesión de dispositivo que necesaria al maestro de copia de seguridad.  
  
 En el ejemplo siguiente se crea una copia de seguridad completa de la base de datos maestra.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Vea también  
 [RESTAURAR la base de datos &#40; Almacenamiento de datos en paralelo &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
