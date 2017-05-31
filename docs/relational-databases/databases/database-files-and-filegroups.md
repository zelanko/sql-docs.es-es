---
title: Archivos y grupos de archivos de base de datos | Microsoft Docs
ms.custom: 
ms.date: 10/11/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d24838e7301cf2b22d812bbcb7ad4e29e793017e
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="database-files-and-filegroups"></a>Archivos y grupos de archivos de base de datos
  Como mínimo, todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen dos archivos del sistema operativo: un archivo de datos y un archivo de registro. Los archivos de datos contienen datos y otros objetos, como tablas, índices, procedimientos almacenados y vistas. Los archivos de registro contienen la información necesaria para recuperar todas las transacciones de la base de datos. Los archivos de datos se pueden agrupar en grupos de archivos para su asignación y administración.  
  
## <a name="database-files"></a>Archivos de la base de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen tres tipos de archivos, tal como se muestra en la tabla siguiente.  
  
|Archivo|Descripción|  
|----------|-----------------|  
|Principal|El archivo de datos principal incluye la información de inicio de la base de datos y apunta a los demás archivos de la misma. Los datos y objetos del usuario se pueden almacenar en este archivo o en archivos de datos secundarios. Cada base de datos tiene un archivo de datos principal. La extensión recomendada para los nombres de archivos de datos principales es .mdf.|  
|Secundario|Los archivos de datos secundarios son opcionales, están definidos por el usuario y almacenan los datos del usuario. Se pueden utilizar para distribuir datos en varios discos colocando cada archivo en una unidad de disco distinta. Además, si una base de datos supera el tamaño máximo establecido para un archivo de Windows, puede utilizar los archivos de datos secundarios para permitir el crecimiento de la base de datos.<br /><br /> La extensión de nombre de archivo recomendada para los archivos de datos secundarios es .ndf.|  
|Registro de transacciones|Los archivos del registro de transacciones contienen la información de registro que se utiliza para recuperar la base de datos. Cada base de datos debe tener al menos un archivo de registro. La extensión recomendada para los nombres de archivos de registro es .ldf.|  
  
 Por ejemplo, puede crearse una base de datos sencilla denominada **Ventas** con un archivo principal que contenga todos los datos y objetos y un archivo de registro con la información del registro de transacciones. Por otra parte, puede crearse una base de datos más compleja, **Pedidos** , compuesta por un archivo principal y cinco archivos secundarios. Los datos y objetos de la base de datos se reparten entre los seis archivos, y cuatro archivos de registro adicionales contienen la información del registro de transacciones.  
  
 De forma predeterminada, los datos y los registros de transacciones se colocan en la misma unidad y ruta de acceso para administrar los sistemas de un solo disco, pero puede que esto no resulte óptimo para los entornos de producción. Se recomienda colocar los archivos de datos y de registro en distintos discos.  

### <a name="logical-and-physical-file-names"></a>Nombres de archivo lógico y físico

Los archivos de SQL Server tienen dos nombres: 

**logical_file_name**  : logical_file_name es el nombre que se usa para hacer referencia al archivo físico en todas las instrucciones Transact-SQL. El nombre de archivo lógico tiene que cumplir las reglas de los identificadores de SQL Server y tiene que ser único entre los nombres de archivos lógicos de la base de datos.

**os_file_name** : os_file_name es el nombre del archivo físico que incluye la ruta de acceso al directorio. Debe seguir las reglas para nombres de archivos del sistema operativo.

Los archivos de datos y de registro de SQL Server se pueden colocar en sistemas de archivos FAT o NTFS. Se recomienda utilizar el sistema de archivos NTFS por las características de seguridad que ofrece. No se pueden colocar grupos de archivos de datos de lectura/escritura, y archivos de registro, en un sistema de archivos NTFS comprimido. Solo las bases de datos de solo lectura y los grupos de archivos secundarios de solo lectura se pueden colocar en un sistema de archivos NTFS comprimido.

Cuando se ejecutan varias instancias de SQL Server en un único equipo, cada instancia recibe un directorio predeterminado diferente para albergar los archivos de las bases de datos creadas en la instancia. Para obtener más información, vea [Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md).

### <a name="data-file-pages"></a>Páginas de archivo de datos

Las páginas de un archivo de datos de SQL Server están numeradas secuencialmente, comenzando por cero (0) para la primera página del archivo. Cada archivo de una base de datos tiene un número de identificador único. Para identificar de forma única una página de una base de datos, se requiere el identificador del archivo y el número de la página. El siguiente ejemplo muestra los números de página de una base de datos que tiene un archivo de datos principal de 4 MB y un archivo de datos secundario de 1 MB.

![data_file_pages](../../relational-databases/databases/media/data-file-pages.gif)

La primera página de cada archivo es una página de encabezado de archivo que contiene información acerca de los atributos del archivo. Algunas de las otras páginas del comienzo del archivo también contienen información de sistema, como mapas de asignación. Una de las páginas de sistema almacenadas en el archivo de datos principal y en el archivo de registro principal es una página de arranque de la base de datos que contiene información acerca de los atributos de la base de datos. Para obtener más información sobre las páginas y los tipos de páginas, vea Descripción de páginas y extensiones.

### <a name="file-size"></a>Tamaño de archivo

Los archivos de SQL Server pueden crecer de forma automática a partir del tamaño especificado inicialmente. Cuando se define un archivo, se puede especificar un incremento de crecimiento. Cada vez que se llena el archivo, el tamaño aumenta en la cantidad especificada. Si hay varios archivos en un grupo de archivos, no crecerán automáticamente hasta que todos los archivos estén llenos. A continuación, el crecimiento tiene lugar por turnos.

Cada archivo también puede tener un tamaño máximo especificado. Si no se especifica un tamaño máximo, el archivo puede crecer hasta utilizar todo el espacio disponible en el disco. Esta característica es especialmente útil cuando SQL Server se usa como una base de datos incrustada en una aplicación para la que el usuario no dispone fácilmente de acceso a un administrador del sistema. El usuario puede dejar que los archivos crezcan automáticamente cuando sea necesario y evitar así las tareas administrativas de supervisar la cantidad de espacio disponible en la base de datos y asignar más espacio manualmente. 


## <a name="database-snapshot-files"></a>Archivos de instantáneas de bases de datos

La forma de archivo que utiliza una instantánea de base de datos para almacenar sus datos de copia por escritura depende de si la instantánea la ha creado un usuario o se utiliza internamente:

* Una instantánea de base de datos que crea un usuario almacena sus datos en uno o más archivos dispersos. La tecnología de archivos dispersos es una característica del sistema de archivos NTFS. Al principio, un archivo disperso no incluye datos de usuario y no se le asigna espacio en disco. Para obtener información general sobre el uso de los archivos dispersos en instantáneas de bases de datos y el crecimiento de estas, vea [Ver el tamaño del archivo disperso de una instantánea de base de datos (Transact-SQL)](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md). 
* Las instantáneas de bases de datos las utilizan internamente algunos comandos DBCC. Entre estos comandos se incluyen: DBCC CHECKDB, DBCC CHECKTABLE, DBCC CHECKALLOC y DBCC CHECKFILEGROUP. Una instantánea de base de datos interna utiliza flujos de datos alternativos dispersos de los archivos de base de datos originales. Como los archivos dispersos, los flujos de datos alternativos son una característica del sistema de archivos NTFS. El uso de los flujos de datos alternativos dispersos permite que varias asignaciones de datos se asocien a un único archivo o carpeta sin afectar a las estadísticas de tamaño o volumen. 


  
## <a name="filegroups"></a>Grupos de archivos  
 Cada base de datos tiene un grupo de archivos principal. Este grupo de archivos contiene el archivo de datos principal y cualquier otro archivo secundario que no se encuentre en otro grupo de archivos. Se pueden crear grupos de archivos definidos por el usuario para agrupar archivos con fines administrativos y de asignación y ubicación de datos.  
  
 Por ejemplo, pueden crearse tres archivos, Datos1.ndf, Datos2.ndf y Datos3.ndf, en tres unidades de disco respectivamente para asignarlos posteriormente al grupo de archivos **grArchivos1**. A continuación, se puede crear una tabla específicamente para el grupo de archivos **grArchivos1**. Las consultas de datos de la tabla se distribuirán por los tres discos, con lo que mejorará el rendimiento. Puede obtenerse la misma mejora del rendimiento con un solo archivo creado en un conjunto de bandas RAID (matriz redundante de discos independientes). No obstante, los archivos y grupos de archivos permiten agregar fácilmente nuevos archivos a discos nuevos.  
  
 Todos los archivos de datos se almacenan en los grupos de archivos que se indican en la tabla siguiente.  
  
|Grupo de archivos|Descripción|  
|---------------|-----------------|  
|Principal|Grupo de archivos que contiene el archivo principal. Todas las tablas del sistema se asignan al grupo de archivos principal.|  
|Definidos por el usuario|Cualquier grupo de archivos creado específicamente por el usuario al crear la base de datos o al modificarla.|  
  
### <a name="default-filegroup"></a>Grupo de archivos predeterminado  
 Cuando se crean objetos en la base de datos sin especificar a qué grupo de archivos pertenecen, se asignan al grupo de archivos predeterminado. Siempre existe un grupo de archivos designado como predeterminado. Los archivos del grupo de archivos predeterminado deben ser lo suficientemente grandes como para dar cabida a todos los objetos nuevos no asignados a otros grupos de archivos.  
  
 El grupo de archivos PRINCIPAL es el predeterminado, a menos que se cambie mediante la instrucción ALTER DATABASE. Los objetos y las tablas del sistema no se asignan al nuevo grupo de archivos predeterminado, sino que siguen asignados al grupo de archivos PRIMARY.  

### <a name="file-and-filegroup-example"></a>Ejemplo de archivos y grupos de archivos

En el siguiente ejemplo se crea una base de datos en una instancia de SQL Server. La base de datos tiene un archivo de datos principal, un grupo de archivos definido por el usuario y el archivo de registro. El archivo de datos principal está en el grupo de archivos principal y el grupo de archivos definido por el usuario tiene dos archivos de datos secundarios. Una instrucción ALTER DATABASE hace que el grupo de archivos definido por el usuario sea el grupo predeterminado. A continuación, se crea una tabla que especifica el grupo de archivos definido por el usuario. (En este ejemplo se usa una ruta de acceso genérica `c:\Program Files\Microsoft SQL Server\MSSQL.1` para evitar que se especifique una versión de SQL Server).

```
USE master;
GO
-- Create the database with the default data
-- filegroup and a log file. Specify the
-- growth increment and the max size for the
-- primary data file.
CREATE DATABASE MyDB
ON PRIMARY
  ( NAME='MyDB_Primary',
    FILENAME=
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_Prm.mdf',
    SIZE=4MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
FILEGROUP MyDB_FG1
  ( NAME = 'MyDB_FG1_Dat1',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_1.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB),
  ( NAME = 'MyDB_FG1_Dat2',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB_FG1_2.ndf',
    SIZE = 1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB)
LOG ON
  ( NAME='MyDB_log',
    FILENAME =
       'c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\data\MyDB.ldf',
    SIZE=1MB,
    MAXSIZE=10MB,
    FILEGROWTH=1MB);
GO
ALTER DATABASE MyDB 
  MODIFY FILEGROUP MyDB_FG1 DEFAULT;
GO

-- Create a table in the user-defined filegroup.
USE MyDB;
CREATE TABLE MyTable
  ( cola int PRIMARY KEY,
    colb char(8) )
ON MyDB_FG1;
GO
```

La siguiente ilustración resume los resultados del ejemplo anterior.

![filegroup_example](../../relational-databases/databases/media/filegroup-example.gif)
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
 [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

