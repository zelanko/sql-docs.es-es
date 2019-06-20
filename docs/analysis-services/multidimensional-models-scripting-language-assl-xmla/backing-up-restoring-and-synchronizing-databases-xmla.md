---
title: Copia de seguridad, restaurar, sincronizar y bases de datos (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19d311a07eb11f1c5119a3c20d7536b5a2986b49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62719886"
---
# <a name="backing-up-restoring-and-synchronizing-databases-xmla"></a>Restaurar, sincronizar y realizar copias de seguridad de bases de datos (XMLA)
  En XML for Analysis, hay tres comandos que sirven para restaurar, sincronizar y realizar copias de seguridad de las bases de datos:  
  
-   El [copia de seguridad](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) comando realiza una copia un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos mediante un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] el archivo de copia de seguridad (.abf), como se describe en la sección, [Backing Up Databases](#backing_up_databases).  
  
-   El [restaurar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) comando restaura un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de base de datos desde un archivo .abf, como se describe en la sección [restaurar bases de datos](#restoring_databases).  
  
-   El [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) comando sincroniza una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de base de datos con los datos y metadatos de otra base de datos, como se describe en la sección [sincronizar bases de datos](#synchronizing_databases).  
  
##  <a name="backing_up_databases"></a> La copia de seguridad de bases de datos  
 Como se mencionó anteriormente, el **copia de seguridad** comando realiza una copia especificado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos a un archivo de copia de seguridad. El **copia de seguridad** comando tiene varias propiedades que permiten especificar la base de datos se copia el archivo de copia de seguridad para usar, cómo realizar copias de seguridad de las definiciones de seguridad y las particiones remotas, una copia de seguridad.  
  
> [!IMPORTANT]  
>  La cuenta de servicio de Analysis Services debe tener permiso para escribir en la ubicación de copia de seguridad especificada para cada archivo. Además, el usuario debe tener uno de los roles siguientes: rol de administrador en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o ser miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos de la que se va a hacer copia de seguridad.  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificar la base de datos y el archivo de copia de seguridad  
 Para especificar la base de datos de una copia de seguridad, establezca el [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) propiedad de la **copia de seguridad** comando. El **objeto** propiedad debe contener un identificador de objeto para una base de datos o se produce un error.  
  
 Para especificar el archivo que se va a ser creadas y usadas por el proceso de copia de seguridad, establezca el [archivo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/file-element-xmla) propiedad de la **copia de seguridad** comando. El **archivo** propiedad debe establecerse en un nombre de ruta de acceso y de UNC para el archivo de copia de seguridad que se va a crear.  
  
 Además de especificar qué archivo se va a utilizar para la copia de seguridad, puede establecer las siguientes opciones para el archivo de copia de seguridad especificado:  
  
-   Si establece la [AllowOverwrite](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/allowoverwrite-element-xmla) en true, el **copia de seguridad** comando sobrescribe el archivo de copia de seguridad si el archivo especificado ya existe. Si establece la **AllowOverwrite** propiedad en false, se produce un error si ya existe el archivo de copia de seguridad especificado.  
  
-   Si establece la [ApplyCompression](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/applycompression-element-xmla) en true, el archivo de copia de seguridad se comprime una vez creado el archivo.  
  
-   Si establece la [contraseña](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/password-element-xmla) propiedad en cualquier valor en blanco, el archivo de copia de seguridad se cifra con la contraseña especificada.  
  
    > [!IMPORTANT]  
    >  Si **ApplyCompression** y **contraseña** propiedades no se especifican, el archivo de copia de seguridad almacena los nombres de usuario y contraseñas que se encuentran en las cadenas de conexión en texto no cifrado. Los datos almacenados en texto no cifrado se pueden recuperar. Para mayor seguridad, utilice el **ApplyCompression** y **contraseña** configuración tanto comprimir y cifrar el archivo de copia de seguridad.  
  
### <a name="backing-up-security-settings"></a>Realizar copias de seguridad de la configuración de seguridad  
 El [seguridad](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) propiedad determina si el **copia de seguridad** comando realiza una copia las definiciones de seguridad, como roles y permisos, definidas en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos. El **seguridad** propiedad determina también si el archivo de copia de seguridad incluye las cuentas de usuario de Windows y grupos definidos como miembros de las definiciones de seguridad.  
  
 El valor de la **seguridad** propiedad está limitada a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad en el archivo de copia de seguridad, pero excluye la información de pertenencia.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de pertenencia en el archivo de copia de seguridad.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad del archivo de copia de seguridad.|  
  
### <a name="backing-up-remote-partitions"></a>Realizar copias de seguridad de particiones remotas  
 Realizar copias de seguridad de las particiones remotas en el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos, Establece la [BackupRemotePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/backupremotepartitions-element-xmla) propiedad de la **copia de seguridad** comando a true. Esta configuración hace que el **copia de seguridad** comando para crear un archivo de copia de seguridad remoto para cada origen de datos remoto que se usa para almacenar las particiones remotas para la base de datos.  
  
 Para que cada origen de datos remoto una copia de seguridad, puede especificar el archivo de copia de seguridad correspondiente mediante la inclusión de un [ubicación](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/location-element-xmla) elemento en el [ubicaciones](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/locations-element-xmla) propiedad de la **copia de seguridad** comando. El **ubicación** elemento debería tener su **archivo** propiedad establecida en el nombre de archivo y ruta UNC del archivo de copia de seguridad remoto y su [DataSourceID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceid-element-xmla) propiedad establecida en el identificador de el origen de datos remoto definido en la base de datos.  
  
##  <a name="restoring_databases"></a> Restaurar bases de datos  
 El **restaurar** comando restaura un especificado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos desde un archivo de copia de seguridad. El **restaurar** comando tiene varias propiedades que permiten especificar la base de datos para restaurar el archivo de copia de seguridad para usar, cómo restaurar definiciones de seguridad, las particiones remotas que se almacenará y la reubicación OLAP relacional (ROLAP) objetos.  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el usuario debe tener una de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o miembro de un rol de la base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
### <a name="specifying-the-database-and-backup-file"></a>Especificar la base de datos y el archivo de copia de seguridad  
 El **DatabaseName** propiedad de la **restaurar** comando debe contener un identificador de objeto para una base de datos o se produce un error. Si la base de datos especificada ya existe, el **AllowOverwrite** propiedad determina si la base de datos existente se sobrescribe. Si el **AllowOverwrite** propiedad está establecida en false y la base de datos especificada ya existe, se produce un error.  
  
 Debe establecer el **archivo** propiedad de la **restaurar** comando a un nombre de archivo y ruta UNC para el archivo de copia de seguridad debe restaurarse en la base de datos especificado. También puede establecer el **contraseña** propiedad para el archivo de copia de seguridad especificado. Si el **contraseña** propiedad está establecida en cualquier valor en blanco, el archivo de copia de seguridad se descifra mediante el uso de la contraseña especificada. Si el archivo de copia de seguridad no está cifrado o la contraseña especificada no coincide con la utilizada para cifrar dicho archivo, se produce un error.  
  
### <a name="restoring-security-settings"></a>Restaurar la configuración de seguridad  
 El **seguridad** propiedad determina si el **restaurar** comando restaura las definiciones de seguridad, como los roles y permisos, definidas en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos. El **seguridad** propiedad también determina si el **restaurar** comando incluye las cuentas de usuario de Windows y grupos definidos como miembros de las definiciones de seguridad como parte del proceso de restauración.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad en la base de datos, pero excluye la información de suscripción.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de pertenencia en la base de datos.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad de la base de datos.|  
  
### <a name="restoring-remote-partitions"></a>Restaurar particiones remotas  
 Para cada archivo de copia de seguridad remoto creado durante una anterior **copia de seguridad** de comandos, puede restaurar su partición remota asociada mediante la inclusión de un **ubicación** elemento en el **ubicaciones**propiedad de la **restaurar** comando. El [DataSourceType](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourcetype-element-xmla) propiedad para cada **ubicación** elemento debe excluirse o bien establece explícitamente en *remoto*.  
  
 Para cada uno especifica **ubicación** elemento, el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia pone en contacto con el origen de datos remoto especificado en el **DataSourceID** propiedad para restaurar las particiones definidas en el archivo de copia de seguridad remoto se especifica en el **archivo** propiedad. Además el **DataSourceID** y **archivo** propiedades, las propiedades siguientes están disponibles para cada **ubicación** elemento utilizado para restaurar una partición remota:  
  
-   Para invalidar la cadena de conexión para el origen de datos remoto especificado en **DataSourceID**, puede establecer el **ConnectionString** propiedad de la **ubicación** elemento a un cadena de conexión diferente. El **restaurar** comando, a continuación, usará la cadena de conexión que se encuentra en la **ConnectionString** propiedad. Si **ConnectionString** no se especifica, el **restaurar** comando usa la cadena de conexión almacenada en el archivo de copia de seguridad para el origen de datos remoto especificado. Puede usar el **ConnectionString** opción para mover una partición remota a una instancia remota diferente. Sin embargo, no puede usar el **ConnectionString** configuración para restaurar una partición remota a la misma instancia que contiene la base de datos restaurada. En otras palabras, no puede usar el **ConnectionString** propiedad que se va a realizar una partición remota en una partición local.  
  
-   Para cada carpeta original utilizada para almacenar las particiones remotas en el origen de datos remoto, puede especificar un [carpeta](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/folder-element-xmla) elemento para indicar la nueva carpeta en la que se va a restaurar todas las particiones remotas almacenadas en la carpeta original. Si un **carpeta** elemento no se especifica, el **restaurar** comando usa las carpetas originales especificadas para las particiones remotas contenidas en el archivo de copia de seguridad remoto.  
  
### <a name="relocating-rolap-objects"></a>Reubicar objetos ROLAP  
 El **restaurar** comando no puede restaurar agregaciones ni datos para los objetos que utilizan el almacenamiento ROLAP, ya que dicha información se almacena en las tablas del origen de datos relacional subyacente. Sin embargo, pueden restaurarse los metadatos de los objetos ROLAP. Para restaurar los metadatos del objeto ROLAP, el **restaurar** comando vuelve a crea la estructura de tabla en un origen de datos relacional.  
  
 Puede usar el **ubicación** elemento en un **restaurar** comando reubicar objetos ROLAP. Para cada **ubicación** elemento utilizado para reubicar un origen de datos, el **DataSourceType** propiedad debe establecerse explícitamente en *Local*. También debe establecer el **ConnectionString** propiedad de la **ubicación** elemento a la cadena de conexión de la nueva ubicación. Durante la restauración, el **restaurar** comando reemplazará la cadena de conexión para el origen de datos identificado por el **DataSourceID** propiedad de la **ubicación** elemento con el valor de la **ConnectionString** propiedad de la **ubicación** elemento.  
  
##  <a name="synchronizing_databases"></a> Sincronizar bases de datos  
 El **Synchronize** comando sincroniza los datos y metadatos de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos con otra base de datos. El **Synchronize** comando tiene varias propiedades que le permiten especificar la base de datos de origen, cómo sincronizar definiciones de seguridad, las particiones remotas que se sincronizarán y la sincronización de objetos ROLAP.  
  
> [!NOTE]  
>  El **Synchronize** se puede ejecutar el comando únicamente por los administradores de servidor y base de datos. Las bases de datos de origen y de destino deben tener el mismo nivel de compatibilidad de base de datos.  
  
### <a name="specifying-the-source-database"></a>Especificar la base de datos de origen  
 El [origen](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) propiedad de la **Synchronize** comando contiene dos propiedades, **ConnectionString** y **objeto**. El **ConnectionString** propiedad contiene la cadena de conexión de la instancia que contiene la base de datos de origen y el **objeto** propiedad contiene el identificador de objeto para la base de datos de origen.  
  
 La base de datos de destino es la base de datos actual para la sesión en el que el **Synchronize** comando se ejecuta.  
  
 Si el **ApplyCompression** propiedad de la **Synchronize** comando se establece en true, la información enviada desde el origen de la base de datos a la base de datos de destino se comprime antes de enviarse.  
  
### <a name="synchronizing-security-settings"></a>Sincronizar la configuración de seguridad  
 El [SynchronizeSecurity](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/security-element-xmla) propiedad determina si el **Synchronize** comando sincroniza las definiciones de seguridad, como los roles y permisos, definidas en la base de datos de origen. El **SynchronizeSecurity** propiedad también determina si el **sincronizar** comando incluye grupos definidos como miembros de las definiciones de seguridad y cuentas de usuario de Windows.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad en la base de datos de destino, pero excluye la información de suscripción.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de pertenencia en la base de datos de destino.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad de la base de datos de destino.|  
  
### <a name="synchronizing-remote-partitions"></a>Sincronizar particiones remotas  
 Para cada origen de datos remoto que existe en la base de datos de origen, puede sincronizar cada partición remota asociada mediante la inclusión de un **ubicación** elemento en el **ubicaciones** propiedad de la  **Sincronizar** comando. Para cada **ubicación** elemento, el **DataSourceType** propiedad debe excluirse o bien establece explícitamente en *remoto*.  
  
 Para definir y conectarse a un origen de datos remoto en la base de datos de destino, el **Synchronize** comando usa la cadena de conexión definida en el **ConnectionString** propiedad de la **ubicación**  elemento. El **Synchronize** comando, a continuación, usa el **DataSourceID** propiedad de la **ubicación** elemento para identificar las particiones remotas para sincronizar. El **Synchronize**comando sincroniza las particiones remotas en el origen de datos remoto especificado en el **DataSourceID** propiedad en la base de datos de origen con el origen de datos remoto especificado en el  **DataSourceID** propiedad en la base de datos de destino.  
  
 Para cada carpeta original utilizada para almacenar las particiones remotas en el origen de datos remoto en la base de datos de origen, también puede especificar un **carpeta** elemento en el **ubicación** elemento. El **carpeta** elemento indica la nueva carpeta para la base de datos de destino en el que se va a sincronizar todas las particiones remotas almacenadas en la carpeta original en el origen de datos remoto. Si un **carpeta** elemento no se especifica, el comando Synchronize utiliza las carpetas originales especificadas para las particiones remotas contenidas en la base de datos de origen.  
  
### <a name="synchronizing-rolap-objects"></a>Sincronizar objetos ROLAP  
 El **Synchronize** comando no puede sincronizar agregaciones ni datos para los objetos que utilizan el almacenamiento ROLAP, ya que dicha información se almacena en las tablas del origen de datos relacional subyacente. Sin embargo, pueden sincronizarse los metadatos de los objetos ROLAP. Para sincronizar los metadatos, el **Synchronize** comando vuelve a crear la estructura de tabla en un origen de datos relacional.  
  
 Puede usar el **ubicación** elemento en un comando Synchronize para sincronizar objetos ROLAP. Para cada **ubicación** elemento utilizado para reubicar un origen de datos, el **DataSourceType** propiedad debe establecerse explícitamente en *Local*. . También debe establecer el **ConnectionString** propiedad de la **ubicación** elemento a la cadena de conexión de la nueva ubicación. Durante la sincronización, el **Synchronize** comando reemplazará la cadena de conexión para el origen de datos identificado por el **DataSourceID** propiedad de la **ubicación** elemento con el valor de la **ConnectionString** propiedad de la **ubicación** elemento.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de copia de seguridad &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla)   
 [Elemento Restore &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
