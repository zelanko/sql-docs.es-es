---
title: MODIFICAR el archivo de base de datos y las opciones de grupo de archivos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ADD FILE
- ADD_FILE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting files
- removing files
- deleting filegroups
- file modifications [SQL Server]
- databases [SQL Server], size
- relocating files
- databases [SQL Server], modifying
- file additions [SQL Server], ALTER DATABASE
- file moving [SQL Server]
- default filegroups
- ALTER DATABASE statement, files and filegroups
- initializing files [SQL Server]
- database files [SQL Server]
- moving files
- filegroups [SQL Server], deleting
- adding filegroups
- adding files
- database filegroups [SQL Server]
- adding log files
- modifying files
- filegroups [SQL Server], adding
- file initialization [SQL Server]
- files [SQL Server], deleting
- files [SQL Server], adding
- databases [SQL Server], moving
ms.assetid: 1f635762-f7aa-4241-9b7a-b51b22292b07
caps.latest.revision: "61"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0672b00cbb7064bdb889908585b4333865ac75c9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-transact-sql-file-and-filegroup-options"></a>MODIFICAR el archivo de base de datos (Transact-SQL) y las opciones de grupo de archivos 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica los archivos y los grupos de archivos asociados a la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Agrega o quita archivos y grupos de archivos de una base de datos y cambia los atributos de una base de datos o sus archivos y grupos de archivos. Para ver otras opciones de ALTER DATABASE, consulte [ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER DATABASE database_name   
{  
    <add_or_modify_files>  
  | <add_or_modify_filegroups>  
}  
[;]  
  
<add_or_modify_files>::=  
{  
    ADD FILE <filespec> [ ,...n ]   
        [ TO FILEGROUP { filegroup_name } ]  
  | ADD LOG FILE <filespec> [ ,...n ]   
  | REMOVE FILE logical_file_name   
  | MODIFY FILE <filespec>  
}  
  
<filespec>::=   
(  
    NAME = logical_file_name    
    [ , NEWNAME = new_logical_name ]   
    [ , FILENAME = {'os_file_name' | 'filestream_path' | 'memory_optimized_data_path' } ]   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB| % ] ]   
    [ , OFFLINE ]  
)   
  
<add_or_modify_filegroups>::=  
{  
    | ADD FILEGROUP filegroup_name   
        [ CONTAINS FILESTREAM | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    | REMOVE FILEGROUP filegroup_name   
    | MODIFY FILEGROUP filegroup_name  
        { <filegroup_updatability_option>  
        | DEFAULT  
        | NAME = new_filegroup_name   
        | { AUTOGROW_SINGLE_FILE | AUTOGROW_ALL_FILES }  
        }  
}  
<filegroup_updatability_option>::=  
{  
    { READONLY | READWRITE }   
    | { READ_ONLY | READ_WRITE }  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
**\<add_or_modify_files >:: =**
  
 Especifica el archivo que se va a agregar, quitar o modificar.  
  
 *database_name*  
 Es el nombre de la base de datos que se va a modificar.  
  
 ADD FILE  
 Agrega un archivo a la base de datos.  
  
 AL grupo de archivos { *filegroup_name* }  
 Especifica el grupo de archivos al que se agrega el archivo especificado. Para mostrar los grupos de archivos actuales y qué grupo de archivos es el valor predeterminado actual, use la [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) vista de catálogo.  
  
 ADD LOG FILE  
 Agrega un archivo de registro a la base de datos especificada.  
  
 REMOVE FILE *nombre_de_archivo_lógico*  
 Quita la descripción del archivo lógico de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y elimina el archivo físico. El archivo no se puede quitar a menos que esté vacío.  
  
 *nombre_de_archivo_lógico*  
 Es el nombre lógico utilizado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se hace referencia al archivo.  
  
> [!WARNING]  
>  Quitar un archivo de base de datos que tiene FILE_SNAPSHOT copias de seguridad asociadas se realizará correctamente, pero no se eliminarán las instantáneas asociadas para evitar que se invalide las copias de seguridad que hace referencia al archivo de base de datos. El archivo se truncará, pero no se eliminará físicamente con el fin de mantener las copias de seguridad FILE_SNAPSHOT intacta. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 MODIFY FILE  
 Especifica el archivo que se debe modificar. Solo un \<filespec > propiedad se puede cambiar a la vez. NOMBRE siempre debe especificarse en el \<especificaciónDeArchivo > para identificar el archivo que se va a modificar. Si se especifica SIZE, el nuevo tamaño debe ser mayor que el tamaño actual del archivo.  
  
 Para modificar el nombre lógico de un archivo de datos o de un archivo de registro, especifique el nombre del archivo lógico que se va a cambiar en la cláusula `NAME` y especifique el nombre lógico nuevo para el archivo en la cláusula `NEWNAME`. Por ejemplo:  
  
```  
MODIFY FILE ( NAME = logical_file_name, NEWNAME = new_logical_name )   
```  
  
 Para mover un archivo de datos o un archivo de registro a otra ubicación, especifique el nombre del archivo lógico actual en la cláusula `NAME` y especifique la ruta y el nombre del archivo del sistema operativo nuevos en la cláusula `FILENAME`. Por ejemplo:  
  
```  
MODIFY FILE ( NAME = logical_file_name, FILENAME = ' new_path/os_file_name ' )  
```  
  
 Si mueve un catálogo de texto completo, especifique la ruta nueva en la cláusula FILENAME. No especifique el nombre del archivo del sistema operativo.  
  
 Para obtener más información, consulte [mover archivos de base de datos](../../relational-databases/databases/move-database-files.md).  
  
 Para un grupo de archivos FILESTREAM, NAME se puede modificar en línea. Aunque FILENAME se puede modificar en línea, el cambio no surtirá efecto hasta que el contenedor se haya reubicado físicamente y se haya apagado y reiniciado el servidor.  
  
 Puede establecer un archivo FILESTREAM en OFFLINE. Cuando un archivo FILESTREAM está sin conexión, su grupo de archivos principal se marcará internamente como sin conexión; por consiguiente, se producirá un error en cualquier intento de acceso a los datos FILESTREAM situados dentro de ese grupo de archivos.  
  
> [!NOTE]  
>  \<add_or_modify_files > opciones no están disponibles en una base de datos independiente.
  
 **\<especificación de archivo >:: =**  
  
 Controla las propiedades de archivo.  
  
 NOMBRE *nombre_de_archivo_lógico*  
 Especifica el nombre lógico del archivo.  
  
 *nombre_de_archivo_lógico*  
 Es el nombre lógico utilizado en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al hacer referencia al archivo.  
  
 NEWNAME *new_logical_file_name*  
 Especifica un nombre lógico nuevo para el archivo.  
  
 *new_logical_file_name*  
 Es el nombre que reemplaza el nombre del archivo lógico existente. El nombre debe ser único dentro de la base de datos y cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). El nombre puede ser una constante Unicode o de caracteres, un identificador regular o un identificador delimitado.  
  
 Nombre de archivo { **'***nombre_de_archivo_de_sistema_operativo***'** | **'***filestream_path* **'** | **'***memory_optimized_data_path***'**}  
 Especifica el nombre de archivo (físico) del sistema operativo.  
  
 ' *nombre_de_archivo_de_sistema_operativo* '  
 Para un grupo de archivos estándar (ROWS), se trata de la ruta de acceso y el nombre de archivo que utiliza el sistema operativo al crear el archivo. El archivo debe residir en el servidor donde esté instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La ruta especificada debe existir antes de ejecutar la instrucción ALTER DATABASE.  
  
 Los parámetros SIZE, MAXSIZE y FILEGROWTH no se pueden establecer si se ha especificado una ruta UNC para el archivo.  
  
> [!NOTE]  
>  Las bases de datos del sistema no pueden residir en directorios de recursos compartidos UNC.  
  
 Los archivos de datos no se pueden utilizar en los sistemas de archivos comprimidos a menos que sean archivos secundarios de solo lectura o si la base de datos es de solo lectura. Los archivos de registro no se deben almacenar en sistemas de archivos comprimidos.  
  
 Si el archivo está en una partición sin formato, *nombre_de_archivo_de_sistema_operativo* debe especificar solo la letra de unidad de una partición sin formato existente. En cada partición sin formato solo se puede colocar un archivo.  
  
 **'** *filestream_path* **'**  
 Para un grupo de archivos FILESTREAM, FILENAME hace referencia a la ruta de acceso donde se almacenarán los datos FILESTREAM. La ruta de acceso hasta la última carpeta debe existir y la última carpeta no debe existir. Por ejemplo, si especifica la ruta de acceso C:\MyFiles\MyFilestreamData, C:\MyFiles debe existir antes de ejecutar ALTER DATABASE, pero la carpeta MyFilestreamData no debe existir.  
  
 Las propiedades SIZE y FILEGROWTH no se aplican a un grupo de archivos FILESTREAM.  
  
 **'** *memory_optimized_data_path* **'**  
 En un grupo de archivos optimizados para memoria, FILENAME hace referencia a una ruta de acceso donde se almacenarán los datos optimizados para memoria. La ruta de acceso hasta la última carpeta debe existir y la última carpeta no debe existir. Por ejemplo, si especifica la ruta de acceso C:\MisArchivos\MisDatos, C:\MisArchivos debe existir para poder ejecutar ALTER DATABASE, pero la carpeta MisDatos no debe existir.  
  
 El grupo de archivos y el archivo (`<filespec>`) se deben crear en la misma instrucción.  
  
 Las propiedades SIZE, MAXSIZE y FILEGROWTH no se aplican a un grupo de archivos optimizados para memoria.  
  
 TAMAÑO *tamaño*  
 Especifica el tamaño del archivo. SIZE no se aplica a los grupos de archivos FILESTREAM.  
  
 *tamaño*  
 Es el tamaño del archivo.  
  
 Cuando se especifica con ADD FILE, *tamaño* es el tamaño inicial del archivo. Cuando se especifica con MODIFY FILE, *tamaño* es el nuevo tamaño del archivo y debe ser mayor que el tamaño del archivo actual.  
  
 Cuando *tamaño* no se proporciona para el archivo principal, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el tamaño del archivo principal de la **modelo** base de datos. Cuando se especifica un archivo de datos secundario o un archivo de registro, pero *tamaño* no se especifica para el archivo, la [!INCLUDE[ssDE](../../includes/ssde-md.md)] hace que el archivo de 1 MB.  
  
 Se pueden utilizar los sufijos KB, MB, GB y TB para especificar kilobytes, megabytes, gigabytes o terabytes. El valor predeterminado es MB. Especifique un número entero y no incluya decimales. Para especificar una fracción de un megabyte, convierta el valor en kilobytes multiplicando el número por 1024. Por ejemplo, especifique 1536 KB en lugar de 1,5 MB (1,5 x 1024 = 1536).  
  
 MAXSIZE { *max_size*| ILIMITADO}  
 Especifica el tamaño de archivo máximo que puede alcanzar el archivo.  
  
 *max_size*  
 Es el tamaño máximo del archivo. Se pueden utilizar los sufijos KB, MB, GB y TB para especificar kilobytes, megabytes, gigabytes o terabytes. El valor predeterminado es MB. Especifique un número entero y no incluya decimales. Si *max_size* no se especifica, el tamaño del archivo aumenta hasta que el disco está lleno.  
  
 UNLIMITED  
 Especifica que el archivo crecerá hasta que el disco esté lleno. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si se especifica un crecimiento ilimitado para un archivo de registro, su tamaño máximo será de 2 TB, y para un archivo de datos será de 16 TB. No hay un tamaño máximo cuando esta opción se especifica para un contenedor de FILESTREAM. Continúa creciendo hasta que el disco se completa.  
  
 FILEGROWTH *growth_increment*  
 Especifica el incremento de crecimiento automático del archivo. El valor FILEGROWTH de un archivo no puede superar el valor MAXSIZE. FILEGROWTH no se aplica a los grupos de archivos FILESTREAM.  
  
 *growth_increment*  
 Es la cantidad de espacio que se agrega al archivo siempre que se necesita más espacio.  
  
 El valor se puede especificar en MB, KB, GB, TB o como porcentaje (%). Si se especifica un número sin los sufijos MB, KB o %, el valor predeterminado es MB. Cuando se especifica %, el incremento de crecimiento es el porcentaje especificado del tamaño del archivo en el momento en que tiene lugar el incremento. El tamaño especificado se redondea al múltiplo de 64 KB más cercano.  
  
 El valor 0 indica que el aumento automático se establece en OFF y no se permite ningún espacio adicional.  
  
 Si no se especifica FILEGROWTH, los valores predeterminados son:  
  
|Versión|Valores predeterminados|  
|-------------|--------------------|  
|Principio[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Datos de 64 MB. Los archivos de registro de 64 MB.|  
|Principio[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Datos de 1 MB. Archivos de registro de 10%.|  
|Antes de[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Datos de 10%. Archivos de registro de 10%.|  
  
 OFFLINE  
 Establece el archivo en modo sin conexión e impide el acceso a todos los objetos del grupo de archivos.  
  
> [!CAUTION]  
>  Utilice esta opción solo si el archivo está dañado y se puede restaurar. Un archivo establecido en OFFLINE solo se puede establecer como en línea mediante la restauración del archivo a partir de una copia de seguridad. Para obtener más información sobre cómo restaurar un único archivo, vea [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
> [!NOTE]  
>  \<especificación de archivo > opciones no están disponibles en una base de datos independiente.  
  
 **\<add_or_modify_filegroups >:: =**  
  
 Agrega, modifica o quita un grupo de archivos de la base de datos.  
  
 Agregar grupo de archivos *filegroup_name*  
 Agrega un grupo de archivos a la base de datos.  
  
 CONTAINS FILESTREAM  
 Especifica que el grupo de archivos almacena objetos binarios grandes (BLOB) de FILESTREAM en el sistema de archivos.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica que el grupo de archivos almacena los datos optimizados para memoria en el sistema de archivos. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Solo se admite un grupo de archivos MEMORY_OPTIMIZED_DATA por cada base de datos. Para crear tablas optimizadas para memoria, el grupo de archivos no puede estar vacío. Debe haber al menos un archivo. *filegroup_name* hace referencia a una ruta de acceso. La ruta de acceso hasta la última carpeta debe existir y la última carpeta no debe existir.  
  
 En el ejemplo siguiente se crea un grupo de archivos que se agrega a una base de datos denominada xtp_db y se agrega un archivo al grupo de archivos. El grupo de archivos almacena los datos optimizados en memoria  
  
```  
ALTER DATABASE xtp_db ADD FILEGROUP xtp_fg CONTAINS MEMORY_OPTIMIZED_DATA;  
GO  
ALTER DATABASE xtp_db ADD FILE (NAME='xtp_mod', FILENAME='d:\data\xtp_mod') TO FILEGROUP xtp_fg;  
```  
  
 Quitar grupo de archivos *filegroup_name*  
 Quita un grupo de archivos de la base de datos. El grupo de archivos no se puede quitar a menos que esté vacío. Quita todos los archivos del primer grupo de archivos. Para obtener más información, vea "REMOVE FILE *nombre_de_archivo_lógico*," anteriormente en este tema.  
  
> [!NOTE]  
>  A menos que el recolector de elementos no utilizados de FILESTREAM haya quitado todos los archivos de un contenedor de FILESTREAM, la operación ALTER DATABASE REMOVE FILE para quitar un contenedor de FILESTREAM no se ejecutará correctamente y devolverá un error. Vea la sección "Quitar un contenedor de FILESTREAM" en el epígrafe Comentarios más adelante en este tema.  
  
MODIFY FILEGROUP *filegroup_name* { \<filegroup_updatability_option > | DEFAULT | NOMBRE  **=**  *new_filegroup_name* } modifica el grupo de archivos al establecer el estado en READ_ONLY o READ_WRITE, establecer el grupo de archivos en el grupo de archivos predeterminado para la base de datos, o cambiar el nombre de grupo de archivos.  
  
 \<filegroup_updatability_option >  
 Establece la propiedad de solo lectura o solo lectura/escritura para el grupo de archivos.  
  
 DEFAULT  
 Cambia el grupo de archivos de base de datos predeterminada a *filegroup_name*. Solo un grupo de archivos de la base de datos puede ser el grupo de archivos predeterminado. Para más información, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 NOMBRE = *new_filegroup_name*  
 Cambia el nombre de grupo de archivos a la *new_filegroup_name*.  
  
 OPCIONES AUTOGROW_SINGLE_FILE  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Cuando un archivo en el grupo de archivos cumple el umbral de crecimiento automático, crece únicamente ese archivo. Ésta es la opción predeterminada.  
  
 AUTOGROW_ALL_FILES  

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Cuando un archivo en el grupo de archivos cumple el umbral de crecimiento automático, crecen todos los archivos en el grupo de archivos.  
  
 **\<filegroup_updatability_option >:: =**  
  
 Establece la propiedad de solo lectura o solo lectura/escritura para el grupo de archivos.  
  
 READ_ONLY | READONLY  
 Especifica que el grupo de archivos es de solo lectura. No se permite la actualización de los objetos del mismo. El grupo de archivos principal no puede ser de solo lectura. Para cambiar este estado, debe tener acceso exclusivo a la base de datos. Para obtener más información, vea la cláusula SINGLE_USER.  
  
 Una base de datos de solo lectura no permite realizar modificaciones en los datos:  
  
-   Se omite la recuperación automática cuando se inicia el sistema.  
  
-   No es posible reducir la base de datos.  
  
-   No se produce ningún bloqueo en las bases de datos de solo lectura. Esto puede acelerar el rendimiento de las consultas.  
  
> [!NOTE]  
>  La palabra clave READONLY se quitará en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite el uso de READONLY en los nuevos trabajos de desarrollo y piense en modificar las aplicaciones que utilizan READONLY actualmente. Utilice READ_ONLY en su lugar.  
  
 READ_WRITE | READWRITE  
 Especifica que el grupo es READ_WRITE. Pueden realizarse actualizaciones en los objetos del grupo de archivos. Para cambiar este estado, debe tener acceso exclusivo a la base de datos. Para obtener más información, vea la cláusula SINGLE_USER.  
  
> [!NOTE]  
>  La palabra clave READWRITE se quitará en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite el uso de READWRITE en los nuevos trabajos de desarrollo y piense en modificar las aplicaciones que utilizan READWRITE actualmente. Utilice READ_WRITE en su lugar.  
  
 El estado de estas opciones se puede determinar mediante el examen de la **is_read_only** columna en el **sys.databases** vista de catálogo o la **Updateability** propiedad de la Función DATABASEPROPERTYEX.  
  
## <a name="remarks"></a>Comentarios  
 Para reducir el tamaño de una base de datos, utilice [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 No se puede agregar o quitar un archivo mientras se está ejecutando una instrucción BACKUP.  
  
 Para cada base de datos pueden especificarse hasta 32.767 archivos y 32.767 grupos de archivos.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior, el estado de un archivo de base de datos (por ejemplo, en línea o sin conexión) se mantiene con independencia del estado de la base de datos. Para obtener más información, consulte [Estados de los archivos](../../relational-databases/databases/file-states.md). El estado de los archivos de un grupo de archivos determina la disponibilidad de todo el grupo de archivos. Para que un grupo de archivos esté disponible, todos los archivos del grupo de archivos deben estar en línea. Si un grupo de archivos se encuentra en modo sin conexión, todos los intentos de acceso al grupo de archivos por parte de una instrucción SQL generan un error. Al generar un plan de consulta para las instrucciones SELECT, el optimizador de consultas evita los índices no clúster y las vistas indizadas que residen en los grupos de archivos sin conexión. Esto permite que las instrucciones se ejecuten correctamente. No obstante, si el grupo de archivos sin conexión contiene el montón o el índice clúster de la tabla de destino, las instrucciones SELECT no funcionarán. Adicionalmente, cualquier instrucción INSERT, UPDATE o DELETE que modifique una tabla con cualquier índice en un grupo de archivos sin conexión no funcionará.  
  
## <a name="moving-files"></a>Mover archivos  
 Puede mover los archivos de sistema, de datos definidos por el usuario o de registro si especifica la ubicación nueva en FILENAME. Esto puede resultar útil en los siguientes escenarios:  
  
-   Recuperación de un error. Por ejemplo, la base de datos está en modo de sospecha o cerrada debido a un error del hardware.  
  
-   Reubicación planeada  
  
-   Reubicación para el mantenimiento planeado del disco  
  
 Para obtener más información, consulte [mover archivos de base de datos](../../relational-databases/databases/move-database-files.md).  
  
## <a name="initializing-files"></a>Inicializar archivos  
 De forma predeterminada, los archivos de datos y registro se inicializan mediante el relleno de los archivos con ceros al realizar una de las siguientes operaciones:  
  
-   Crear una base de datos  
  
-   Agregar archivos a una base de datos existente  
  
-   Aumentar el tamaño de un archivo existente  
  
-   Restaurar una base de datos o un grupo de archivos  
  
 Los archivos de datos se pueden inicializar de forma instantánea. Esto permite la ejecución rápida de estas operaciones con los archivos.  
  
## <a name="removing-a-filestream-container"></a>Quitar un contenedor de FILESTREAM  
 Aunque un contenedor de FILESTREAM puede haberse vaciado utilizando la operación "DBCC SHRINKFILE", la base de datos puede seguir necesitando mantener las referencias a los archivos eliminados por diversas razones de mantenimiento del sistema. [sp_filestream_force_garbage_collection &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) se ejecutará el recolector de elementos no utilizados de FILESTREAM para quitar estos archivos cuándo es seguro hacerlo. A menos que el recolector de elementos no utilizados de FILESTREAM se quita todos los archivos de un contenedor de FILESTREAM, la operación de modificar el archivo de base de DATOSQUITAR se producirá un error al quitar un contenedor FILESTREAM y devolverá un error. Se recomienda el siguiente proceso para quitar un contenedor de FILESTREAM.  
  
1.  Ejecutar [DBCC SHRINKFILE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) con la opción EMPTYFILE para mover el contenido activo de este contenedor a otros contenedores.  
  
2.  Asegúrese de que se han tomado copias de seguridad de registros en el modelo de recuperación FULL o BULK_LOGGED.  
  
3.  Asegúrese de que se ha ejecutado el trabajo del lector del registro de replicación, si es pertinente.  
  
4.  Ejecutar [sp_filestream_force_garbage_collection &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md) para forzar que el recolector de elementos no utilizados a eliminar los archivos que ya no son necesarios en este contenedor.  
  
5.  Ejecute ALTER DATABASE con la opción REMOVE FILE para quitar este contenedor.  
  
6.  Repita los pasos 2 a 4 una vez más para completar la recolección de elementos no utilizados.  
  
7.  Utilice ALTER Database...REMOVE FILE para quitar este contenedor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-adding-a-file-to-a-database"></a>A. Agregar un archivo a una base de datos  
 En el siguiente ejemplo se agrega un archivo de datos de 5 MB a la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD FILE   
(  
    NAME = Test1dat2,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat2.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
);  
GO  
  
```  
  
### <a name="b-adding-a-filegroup-with-two-files-to-a-database"></a>B. Agregar a una base de datos un grupo de archivos con dos archivos  
 En el ejemplo siguiente se crea el grupo de archivos `Test1FG1` en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] la base de datos y agrega dos archivos de 5 MB al grupo de archivos.  
  
```  
USE master  
GO  
ALTER DATABASE AdventureWorks2012  
ADD FILEGROUP Test1FG1;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD FILE   
(  
    NAME = test1dat3,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat3.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
),  
(  
    NAME = test1dat4,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat4.ndf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
)  
TO FILEGROUP Test1FG1;  
GO  
  
```  
  
### <a name="c-adding-two-log-files-to-a-database"></a>C. Agregar dos archivos de registro a una base de datos  
 En el siguiente ejemplo se agregan dos archivos de registro de 5 MB a la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
ADD LOG FILE   
(  
    NAME = test1log2,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\test2log.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
),  
(  
    NAME = test1log3,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\DATA\test3log.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 100MB,  
    FILEGROWTH = 5MB  
);  
GO  
  
```  
  
### <a name="d-removing-a-file-from-a-database"></a>D. Quitar un archivo de una base de datos  
 En el siguiente ejemplo se quita uno de los archivos agregados en el ejemplo B.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4;  
GO  
  
```  
  
### <a name="e-modifying-a-file"></a>E. Modificar un archivo  
En el siguiente ejemplo aumenta el tamaño de uno de los archivos agregados en el ejemplo B.  
 La instrucción ALTER DATABASE con el comando MODIFY FILE sólo puede realizar un tamaño de archivo más grande, por lo que si tiene que reducir el tamaño del archivo debe usar DBCC SHRINKFILE.  
  
```  
USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO  
```

En este ejemplo se reduce el tamaño de un archivo de datos a 100 MB y, a continuación, especifica el tamaño en esa cantidad. 

```
USE AdventureWorks2012;
GO

DBCC SHRINKFILE (AdventureWorks2012_data, 100);
GO

USE master;  
GO
  
ALTER DATABASE AdventureWorks2012   
MODIFY FILE  
(NAME = test1dat3,  
SIZE = 200MB);  
GO
```
 
  
### <a name="f-moving-a-file-to-a-new-location"></a>F. Mover un archivo a otra ubicación  
 En el siguiente ejemplo se mueve el archivo `Test1dat2` creado en el ejemplo A a otro directorio.  
  
> [!NOTE]  
>  Debe mover físicamente el archivo al directorio nuevo antes de ejecutar este ejemplo. A continuación, detenga e inicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o establezca la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en OFFLINE y después en ONLINE para implementar el cambio.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
MODIFY FILE  
(  
    NAME = Test1dat2,  
    FILENAME = N'c:\t1dat2.ndf'  
);  
GO  
```  
  
### <a name="g-moving-tempdb-to-a-new-location"></a>G. Mover tempdb a otra ubicación  
 En el siguiente ejemplo se mueve `tempdb` de su ubicación actual en el disco a otra ubicación del disco. Puesto que `tempdb` se vuelve a crear cada vez que se inicia el servicio MSSQLSERVER, no es necesario mover físicamente los archivos de datos y de registro. Los archivos se crean cuando se reinicia el servicio en el paso 3. Hasta que se reinicie el servicio, `tempdb` continúa funcionando en su ubicación existente.  
  
1.  Determine los nombres de archivo lógico de la `tempdb` base de datos y su ubicación actual en el disco.  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    GO  
    ```  
  
2.  Cambie la ubicación de cada archivo con `ALTER DATABASE`.  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE tempdb   
    MODIFY FILE (NAME = tempdev, FILENAME = 'E:\SQLData\tempdb.mdf');  
    GO  
    ALTER DATABASE  tempdb   
    MODIFY FILE (NAME = templog, FILENAME = 'E:\SQLData\templog.ldf');  
    GO  
    ```  
  
3.  Detenga y reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Compruebe el cambio de los archivos.  
  
    ```  
    SELECT name, physical_name  
    FROM sys.master_files  
    WHERE database_id = DB_ID('tempdb');  
    ```  
  
5.  Elimine los archivos tempdb.mdf y templog.ldf de su ubicación original.  
  
### <a name="h-making-a-filegroup-the-default"></a>H. Establecer un grupo de archivos como predeterminado  
 En el ejemplo siguiente se realiza la `Test1FG1` grupo de archivos creada en el ejemplo B el grupo de archivos predeterminado. A continuación, el grupo de archivos predeterminado se restablece al grupo de archivos `PRIMARY`. Tenga en cuenta que `PRIMARY` se debe delimitar con corchetes o comillas.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012   
MODIFY FILEGROUP Test1FG1 DEFAULT;  
GO  
ALTER DATABASE AdventureWorks2012   
MODIFY FILEGROUP [PRIMARY] DEFAULT;  
GO  
  
```  
  
### <a name="i-adding-a-filegroup-using-alter-database"></a>I. Agregar un grupo de archivos mediante ALTER DATABASE  
 En el ejemplo siguiente se agrega un `FILEGROUP` que contiene la cláusula `FILESTREAM` a la base de datos `FileStreamPhotoDB`.  
  
```  
--Create and add a FILEGROUP that CONTAINS the FILESTREAM clause to  
--the FileStreamPhotoDB database.  
ALTER DATABASE FileStreamPhotoDB  
ADD FILEGROUP TodaysPhotoShoot  
CONTAINS FILESTREAM;  
GO  
  
--Add a file for storing database photos to FILEGROUP   
ALTER DATABASE FileStreamPhotoDB  
ADD FILE  
(  
    NAME= 'PhotoShoot1',  
    FILENAME = 'C:\Users\Administrator\Pictures\TodaysPhotoShoot.ndf'  
)  
TO FILEGROUP TodaysPhotoShoot;  
GO  
```      
        
### <a name="j-change-filegroup-so-that-when-a-file-in-the-filegroup-meets-the-autogrow-threshold-all-files-in-the-filegroup-grow"></a>J. Cambie el grupo de archivos para que cuando un archivo en el grupo de archivos cumple el umbral de crecimiento automático, todos los archivos en el grupo de archivos aumentar.
 El ejemplo siguiente genera la necesarios `ALTER DATABASE` instrucciones para modificar grupos de archivos de lectura / escritura con el `AUTOGROW_ALL_FILES` configuración.  
  
```  
--Generate ALTER DATABASE ... MODIFY FILEGROUP statements  
--so that all read-write filegroups grow at the same time.  
SET NOCOUNT ON;

DROP TABLE IF EXISTS #tmpdbs
CREATE TABLE #tmpdbs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, isdone bit);

DROP TABLE IF EXISTS #tmpfgs
CREATE TABLE #tmpfgs (id int IDENTITY(1,1), [dbid] int, [dbname] sysname, fgname sysname, isdone bit);

INSERT INTO #tmpdbs ([dbid], [dbname], [isdone])
SELECT database_id, name, 0 FROM master.sys.databases (NOLOCK) WHERE is_read_only = 0 AND state = 0;

DECLARE @dbid int, @query VARCHAR(1000), @dbname sysname, @fgname sysname

WHILE (SELECT COUNT(id) FROM #tmpdbs WHERE isdone = 0) > 0
BEGIN
    SELECT TOP 1 @dbname = [dbname], @dbid = [dbid] FROM #tmpdbs WHERE isdone = 0

    SET @query = 'SELECT ' + CAST(@dbid AS NVARCHAR) + ', ''' + @dbname + ''', [name], 0 FROM [' + @dbname + '].sys.filegroups WHERE [type] = ''FG'' AND is_read_only = 0;'
    INSERT INTO #tmpfgs
    EXEC (@query)

    UPDATE #tmpdbs
    SET isdone = 1
    WHERE [dbid] = @dbid
END;

IF (SELECT COUNT(ID) FROM #tmpfgs) > 0
BEGIN
    WHILE (SELECT COUNT(id) FROM #tmpfgs WHERE isdone = 0) > 0
    BEGIN
        SELECT TOP 1 @dbname = [dbname], @dbid = [dbid], @fgname = fgname FROM #tmpfgs WHERE isdone = 0

        SET @query = 'ALTER DATABASE [' + @dbname + '] MODIFY FILEGROUP [' + @fgname + '] AUTOGROW_ALL_FILES;'

        PRINT @query

        UPDATE #tmpfgs
        SET isdone = 1
        WHERE [dbid] = @dbid AND fgname = @fgname
    END
END; 
GO  
```      
  
## <a name="see-also"></a>Vea también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [Sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [Sys.FileGroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys.master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Binary Large Object &#40;Blob&#41; Data &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)   
 [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
  
  
