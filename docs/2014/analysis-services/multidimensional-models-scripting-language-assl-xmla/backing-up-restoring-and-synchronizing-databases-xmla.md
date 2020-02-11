---
title: Realizar copias de seguridad, restaurar y sincronizar bases de datos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- restoring databases [XML for Analysis]
- backing up databases [XML for Analysis]
- database backups [XML for Analysis]
- synchronization [XML for Analysis]
- database restores [XML for Analysis]
ms.assetid: 6c021b2e-6ad0-444e-b23f-4b5f72ce084b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6163a538c4e8872016f7ec572e4c177cfe92de94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702277"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Restaurar, sincronizar y realizar copias de seguridad de bases de datos (XMLA)
  En XML for Analysis, hay tres comandos que sirven para restaurar, sincronizar y realizar copias de seguridad de las bases de datos:  
  
-   El [comando backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) realiza una copia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] seguridad de una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos mediante un archivo de copia de seguridad (. ABF), tal como se describe en la sección [copia de seguridad de bases de datos](#backing_up_databases).  
  
-   El comando [restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) restaura una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos a partir de un archivo. ABF, como se describe en la sección [restaurar bases](#restoring_databases)de datos.  
  
-   El comando [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) sincroniza una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos con los datos y metadatos de otra base de datos, como se describe en la sección [sincronizar bases](#synchronizing_databases)de datos.  
  
##  <a name="backing_up_databases"></a>Realizar copias de seguridad de bases de datos  
 Como ya se ha mencionado anteriormente, el comando `Backup` realiza una copia de seguridad de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada en un archivo de copia de seguridad. El comando `Backup` tiene varias propiedades que permiten especificar la base de datos de la que se va a hacer la copia de seguridad, el archivo de copia de seguridad que se va a usar, cómo hacer una copia de seguridad de las definiciones de seguridad y las particiones remotas de las que se va a hacer la copia de seguridad.  
  
> [!IMPORTANT]  
>  La cuenta de servicio de Analysis Services debe tener permiso para escribir en la ubicación de copia de seguridad especificada para cada archivo. Además, el usuario debe tener uno de los roles siguientes: rol de administrador en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o ser miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos de la que se va a hacer copia de seguridad.  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificar la base de datos y el archivo de copia de seguridad  
 Para especificar la base de datos de la que se va a realizar [](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) la copia de seguridad `Backup` , establezca la propiedad Object del comando. La propiedad `Object` debe contener un identificador de objeto para una base de datos; de lo contrario, se produce un error.  
  
 Para especificar el archivo que va a crear y usar el proceso de copia de seguridad, establezca la propiedad [File](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) del `Backup` comando. Para crear el archivo de copia de seguridad, debe establecerse una ruta UNC y un nombre de archivo para la propiedad `File`.  
  
 Además de especificar qué archivo se va a utilizar para la copia de seguridad, puede establecer las siguientes opciones para el archivo de copia de seguridad especificado:  
  
-   Si establece la propiedad [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) en true, el `Backup` comando sobrescribe el archivo de copia de seguridad si el archivo especificado ya existe. Si establece la propiedad `AllowOverwrite` en false, se produce un error si el archivo de copia de seguridad especificado ya existe.  
  
-   Si establece la propiedad [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) en true, el archivo de copia de seguridad se comprime una vez creado el archivo.  
  
-   Si establece la propiedad [password](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) en cualquier valor que no esté en blanco, el archivo de copia de seguridad se cifra con la contraseña especificada.  
  
    > [!IMPORTANT]  
    >  Si no se especifican las propiedades `ApplyCompression` y `Password`, el archivo de copia de seguridad almacena en texto no cifrado los nombres de usuario y las contraseñas que se incluyen en las cadenas de conexión. Los datos almacenados en texto no cifrado se pueden recuperar. Para mayor seguridad, utilice los valores `ApplyCompression` y `Password` a fin de comprimir y cifrar el archivo de copia de seguridad.  
  
### <a name="backing-up-security-settings"></a>Realizar copias de seguridad de la configuración de seguridad  
 La propiedad de [seguridad](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) determina si `Backup` el comando realiza una copia de seguridad de las definiciones de seguridad, como roles y permisos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , definidas en una base de datos. La propiedad `Security` también determina si el archivo de copia de seguridad incluye las cuentas de usuario de Windows y los grupos definidos como miembros de las definiciones de seguridad.  
  
 El valor de la propiedad `Security` se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad en el archivo de copia de seguridad, pero excluye la información de pertenencia.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de pertenencia en el archivo de copia de seguridad.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad del archivo de copia de seguridad.|  
  
### <a name="backing-up-remote-partitions"></a>Realizar copias de seguridad de particiones remotas  
 Para realizar una copia de seguridad de las [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] particiones remotas en la base de datos `Backup` , establezca la propiedad [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) del comando en true. Esta configuración hace que el comando `Backup` cree un archivo de copia de seguridad remoto para cada origen de datos remoto que se utiliza para almacenar particiones remotas de la base de datos.  
  
 Para cada origen de datos remoto del que se va a realizar una copia de seguridad, puede especificar su correspondiente archivo de copia de seguridad incluyendo un elemento `Backup` [Location](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) en la propiedad [locations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) del comando. El `Location` elemento debe tener su `File` propiedad establecida en la ruta de acceso UNC y el nombre de archivo del archivo de copia de seguridad remoto, y su propiedad [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) establecida en el identificador del origen de datos remoto definido en la base de datos.  
  
##  <a name="restoring_databases"></a>Restaurar bases de datos  
 El comando `Restore` restaura una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada a partir de un archivo de copia de seguridad. El comando `Restore` tiene varias propiedades que permiten especificar la base de datos que se va a restaurar, el archivo de copia de seguridad que se va a utilizar, cómo restaurar definiciones de seguridad, las particiones remotas que se van a almacenar y la reubicación de objetos OLAP relacionales (ROLAP).  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el usuario debe tener una de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o miembro de un rol de la base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificar la base de datos y el archivo de copia de seguridad  
 La propiedad `DatabaseName` del comando `Restore` debe contener un identificador de objeto para una base de datos; de lo contrario, se produce un error. Si la base de datos especificada ya existe, la propiedad `AllowOverwrite` determina si se sobrescribe la base de datos existente. Si la propiedad `AllowOverwrite` se establece en false y la base de datos especificada ya existe, se produce un error.  
  
 Para que el archivo de copia de seguridad se restaure en la base de datos especificada, debe establecer la propiedad `File` del comando `Restore` en una ruta UNC y un nombre de archivo. También puede establecer la propiedad `Password` para el archivo de copia de seguridad especificado. Si se establece la propiedad `Password` en cualquier valor que no esté en blanco, el archivo de copia de seguridad se descifra con la contraseña especificada. Si el archivo de copia de seguridad no está cifrado o la contraseña especificada no coincide con la utilizada para cifrar dicho archivo, se produce un error.  
  
### <a name="restoring-security-settings"></a>Restaurar la configuración de seguridad  
 La propiedad `Security` determina si el comando `Restore` restaura las definiciones de seguridad, como roles y permisos, definidas en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La propiedad `Security` también determina si el comando `Restore` incluye las cuentas de usuario de Windows y los grupos definidos como miembros de las definiciones de seguridad como parte del proceso de restauración.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad en la base de datos, pero excluye la información de suscripción.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de pertenencia en la base de datos.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad de la base de datos.|  
  
### <a name="restoring-remote-partitions"></a>Restaurar particiones remotas  
 Para restaurar la partición remota asociada a cada archivo de copia de seguridad remoto creado durante la ejecución anterior de un comando `Backup`, incluya un elemento `Location` en la propiedad `Locations` del comando `Restore`. La propiedad [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) de cada `Location` elemento se debe excluir o establecer explícitamente en *remoto*.  
  
 Por cada elemento `Location` especificado, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se pone en contacto con el origen de datos remoto especificado en la propiedad `DataSourceID` para restaurar las particiones definidas en el archivo de copia de seguridad remoto especificado en la propiedad `File`. Además de las propiedades `DataSourceID` y `File`, para cada elemento `Location` utilizado para restaurar una partición remota están disponibles las siguientes propiedades:  
  
-   Para invalidar la cadena de conexión del origen de datos remoto especificado en `DataSourceID`, puede establecer la propiedad `ConnectionString` del elemento `Location` en una cadena de conexión distinta. A continuación, el comando `Restore` utilizará la cadena de conexión contenida en la propiedad `ConnectionString`. Si no se especifica `ConnectionString`, el comando `Restore` utiliza la cadena de conexión almacenada en el archivo de copia de seguridad para el origen de datos remoto especificado. Puede utilizar el valor `ConnectionString` para mover una partición remota a otra instancia remota distinta. Sin embargo, no puede utilizar el valor `ConnectionString` para restaurar una partición remota en la misma instancia que contiene la base de datos restaurada. En otras palabras, no puede utilizar la propiedad `ConnectionString` para realizar una partición remota en una partición local.  
  
-   Para cada carpeta original utilizada para almacenar las particiones remotas en el origen de datos remoto, puede especificar un elemento de [carpeta](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) para indicar la nueva carpeta en la que se restaurarán todas las particiones remotas almacenadas en la carpeta original. Si no se especifica un elemento `Folder`, el comando `Restore` utiliza las carpetas originales especificadas para las particiones remotas contenidas en el archivo de copia de seguridad remoto.  
  
### <a name="relocating-rolap-objects"></a>Reubicar objetos ROLAP  
 El comando `Restore` no puede restaurar agregaciones ni datos para los objetos que utilizan el almacenamiento ROLAP, ya que dicha información se almacena en tablas en un origen de datos relacional subyacente. Sin embargo, pueden restaurarse los metadatos de los objetos ROLAP. Para restaurar los metadatos del objeto ROLAP, el comando `Restore` vuelve a crear la estructura de tabla en un origen de datos relacional.  
  
 Puede utilizar el elemento `Location` en un comando `Restore` para reubicar los objetos ROLAP. Para cada `Location` elemento que se usa para reubicar un origen `DataSourceType` de datos, la propiedad debe establecerse explícitamente en *local*. Asimismo, tiene que establecer la propiedad `ConnectionString` del elemento `Location` en la cadena de conexión de la nueva ubicación. Durante la restauración, el comando `Restore` reemplazará la cadena de conexión del origen de datos identificado para la propiedad `DataSourceID` del elemento `Location` por el valor de la propiedad `ConnectionString` del elemento `Location`.  
  
##  <a name="synchronizing_databases"></a>Sincronizar bases de datos  
 El comando `Synchronize` sincroniza los datos y metadatos de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada con otra base de datos. El comando `Synchronize` tiene varias propiedades que permiten especificar la base de datos de origen, cómo sincronizar definiciones de seguridad, las particiones remotas que se van a sincronizar y la sincronización de los objetos ROLAP.  
  
> [!NOTE]  
>  Solamente pueden ejecutar el comando `Synchronize` los administradores de servidor y los administradores de bases de datos. Las bases de datos de origen y de destino deben tener el mismo nivel de compatibilidad de base de datos.  
  
### <a name="specifying-the-source-database"></a>Especificar la base de datos de origen  
 La propiedad [source](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) del `Synchronize` comando contiene dos propiedades, `ConnectionString` y. `Object` La propiedad `ConnectionString` contiene la cadena de conexión de la instancia que contiene la base de datos de origen y la propiedad `Object` contiene el identificador de objeto para la base de datos de origen.  
  
 La base de datos de destino es la base de datos activa en la sesión en la que se ejecuta el comando `Synchronize`.  
  
 Si la propiedad `ApplyCompression` del comando `Synchronize` se establece en true, la información enviada desde la base de datos de origen a la base de datos de destino se comprime antes de enviarse.  
  
### <a name="synchronizing-security-settings"></a>Sincronizar la configuración de seguridad  
 La propiedad [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) determina si el `Synchronize` comando sincroniza las definiciones de seguridad, como roles y permisos, definidas en la base de datos de origen. La propiedad `SynchronizeSecurity` también determina si el comando `Sychronize` incluye las cuentas de usuario de Windows y los grupos definidos como miembros de las definiciones de seguridad.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Value|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad en la base de datos de destino, pero excluye la información de suscripción.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de pertenencia en la base de datos de destino.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad de la base de datos de destino.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizar particiones remotas  
 Para sincronizar la partición remota asociada a cada origen de datos remoto existente en la base de datos de origen, incluya un elemento `Location` en la propiedad `Locations` del comando `Synchronize`. Para cada `Location` elemento, la `DataSourceType` propiedad debe estar excluida o establecida explícitamente en *remoto*.  
  
 Para definir un origen de datos remoto en la base de datos de destino y conectarse a éste, el comando `Synchronize` utiliza la cadena de conexión definida en la propiedad `ConnectionString` del elemento `Location`. A continuación, el comando `Synchronize` utiliza la propiedad `DataSourceID` del elemento `Location` para identificar las particiones remotas que se van a sincronizar. El `Synchronize`comando sincroniza las particiones remotas del origen de datos remoto especificado en la `DataSourceID` propiedad en la base de datos de origen con el origen de datos `DataSourceID` remoto especificado en la propiedad en la base de datos de destino.  
  
 También puede especificar un elemento `Folder` en el elemento `Location` por cada carpeta original utilizada para almacenar las particiones remotas del origen de datos remoto en la base de datos de origen. El elemento `Folder` indica la nueva carpeta de la base de datos de destino en la que se van a sincronizar todas las particiones remotas almacenadas en la carpeta original del origen de datos remoto. Si no se especifica un elemento `Folder`, el comando Synchronize utiliza las carpetas originales especificadas para las particiones remotas contenidas en la base de datos de origen.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizar objetos ROLAP  
 El comando `Synchronize` no puede sincronizar agregaciones ni datos para los objetos que utilizan el almacenamiento ROLAP, ya que dicha información se almacena en tablas en un origen de datos relacional subyacente. Sin embargo, pueden sincronizarse los metadatos de los objetos ROLAP. Para sincronizar los metadatos, el comando `Synchronize` vuelve a crear la estructura de tabla en un origen de datos relacional.  
  
 Puede utilizar el elemento `Location` en un comando Synchronize para sincronizar los objetos ROLAP. Para cada `Location` elemento que se usa para reubicar un origen `DataSourceType` de datos, la propiedad debe establecerse explícitamente en *local*. . Asimismo, tiene que establecer la propiedad `ConnectionString` del elemento `Location` en la cadena de conexión de la nueva ubicación. Durante la sincronización, el comando `Synchronize` reemplazará la cadena de conexión del origen de datos identificado para la propiedad `DataSourceID` del elemento `Location` por el valor de la propiedad `ConnectionString` del elemento `Location`.  
  
## <a name="see-also"></a>Consulte también  
 [Elemento backup &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Elemento restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
