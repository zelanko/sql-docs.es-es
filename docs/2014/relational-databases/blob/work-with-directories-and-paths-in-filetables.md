---
title: Trabajar con directorios y rutas de acceso de FileTables | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca25b7c537c333d6bc9eb7745ea2ec6ad6055c4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920026"
---
# <a name="work-with-directories-and-paths-in-filetables"></a>Trabajar con directorios y rutas de acceso de FileTables
  Describe la estructura de directorios en la que los archivos se almacenan en FileTables.  
  
##  <a name="HowToDirectories"></a> Cómo: Trabajar con directorios y rutas de acceso de FileTables  
 Puede usar las tres funciones que se indican a continuación para trabajar con directorios de FileTable en [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
|Para obtener este resultado|Use esta función|  
|------------------------|-----------------------|  
|Obtener la ruta de acceso UNC en el nivel de raíz de una FileTable específica o de la base de datos actual.|[FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|  
|Obtener una ruta de acceso UNC absoluta o relativa de un archivo o directorio de una FileTable.|[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|  
|Obtener el valor del identificador del localizador de ruta de acceso del archivo o directorio especificado en una FileTable proporcionando la ruta de acceso.|[GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|  
  
##  <a name="BestPracticeRelativePaths"></a> Cómo: Usar rutas de acceso relativas para el código Portable  
 Para mantener independientes del equipo y de la base de datos actuales el código y las aplicaciones, evite escribir código basado en rutas de acceso absolutas de archivos. En su lugar, obtenga la ruta de acceso completa de un archivo en tiempo de ejecución usando conjuntamente las funciones [FileTableRootPath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql) y [GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql), como se muestra en el siguiente ejemplo. De forma predeterminada, la función `GetFileNamespacePath` devuelve la ruta de acceso relativa del archivo en la ruta de acceso raíz de la base de datos.  
  
```sql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="restrictions"></a> Restricciones relevantes  
  
###  <a name="nesting"></a> Nivel de anidamiento  
  
> [!IMPORTANT]  
>  No puede almacenar más de 15 niveles de subdirectorios en el directorio de FileTable. Si se almacenan 15 niveles de subdirectorios, el nivel inferior no podrá contener los archivos, ya que estos archivos representarían un nivel adicional.  
  
###  <a name="fqnlength"></a> Longitud del nombre completo de la ruta de acceso  
  
> [!IMPORTANT]  
>  El sistema de archivos NTFS admite nombres de ruta de acceso con una longitud mayor que el límite de 260 caracteres del shell de Windows y la mayoría de las API de Windows. Por consiguiente, es posible que al crear archivos en la jerarquía de archivos de un objeto FileTable con Transact-SQL no pueda verlos ni abrirlos con el Explorador de Windows o muchas otras aplicaciones Windows, porque el nombre completo de la ruta de acceso supera los 260 caracteres. Sin embargo, puede seguir teniendo acceso a estos archivos mediante Transact-SQL.  
  
##  <a name="fullpath"></a> Ruta de acceso completa a un elemento almacenado en una FileTable  
 La ruta de acceso completa a un archivo o directorio almacenado en una FileTable comienza con los elementos siguientes:  
  
1.  El recurso compartido habilitado para el acceso de E/S de archivos de FILESTREAM en el nivel de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  El valor de **DIRECTORY_NAME** especificado en el nivel de la base de datos.  
  
3.  El valor de **FILETABLE_DIRECTORY** especificado en el nivel de FileTable.  
  
 La jerarquía resultante ofrece el siguiente aspecto:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 Esta jerarquía de directorios constituye la raíz del espacio de nombres de archivo de FileTable. En esta jerarquía de directorios, los datos de FILESTREAM de la FileTable se almacenan como archivos y como subdirectorios, que, a su vez, pueden contener archivos y subdirectorios.  
  
 Es importante tener en cuenta que la jerarquía de directorios creada en el recurso compartido de FILESTREAM en el nivel de instancia es una jerarquía de directorios virtual. Esta jerarquía se almacena en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no se representa físicamente en el sistema de archivos NTFS. Todas las operaciones que tienen acceso a los archivos y directorios situados en el recurso compartido de FILESTREAM y en las FileTables que contiene se interceptan y controlan mediante un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incrustado en el sistema de archivos.  
  
##  <a name="roots"></a> Semántica de los directorios raíz en los niveles de instancia, base de datos y FileTable  
 Esta jerarquía de directorios se ajusta a la semántica siguiente:  
  
-   El recurso compartido de FILESTREAM en el nivel de instancia lo configura un administrador y se almacena como una propiedad del servidor. Puede cambiar el nombre de este recurso compartido a través del Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Una operación de cambio de nombre no surtirá efecto hasta que se reinicie el servidor.  
  
-   El valor de **DIRECTORY_NAME** en el nivel de base de datos es NULL de manera predeterminada cuando se crea una nueva base de datos. Un administrador puede establecer o cambiar este nombre mediante la instrucción **ALTER DATABASE** . El nombre debe ser único (en una comparación sin distinción entre mayúsculas y minúsculas) en esa instancia.  
  
-   Normalmente, proporcionará el nombre **FILETABLE_DIRECTORY** como parte de la instrucción **CREATE TABLE** cuando cree un objeto FileTable. Puede cambiar este nombre mediante el comando **ALTER TABLE** .  
  
-   No puede cambiar el nombre de estos directorios raíz a través de operaciones de E/S de archivos.  
  
-   No puede abrir estos directorios raíz con identificadores de archivo exclusivos.  
  
##  <a name="is_directory"></a> Columna is_directory del esquema de la FileTable  
 En la siguiente tabla se describe la interacción entre la columna **is_directory** y la columna **file_stream** que contiene los datos FILESTREAM de un objeto FileTable.  
  
||||  
|-|-|-|  
|*is_directory* **is_directory**|*file_stream* **is_directory**|**Comportamiento**|  
|FALSE|NULL|Esta combinación no es válida y la detectará una restricción definida por el sistema.|  
|FALSE|\<valor>|El elemento representa un archivo.|  
|TRUE|NULL|El elemento representa un directorio.|  
|TRUE|\<valor>|Esta combinación no es válida y la detectará una restricción definida por el sistema.|  
  
##  <a name="alwayson"></a> Usar nombres de red virtual (VNN) con grupos de disponibilidad AlwaysOn  
 Cuando la base de datos que contiene datos de FILESTREAM o FileTable pertenece a un grupo de disponibilidad AlwaysOn:  
  
-   Las funciones FILESTREAM y FileTable aceptan o devuelven nombres de red virtual (VNN) en lugar de nombres de equipo. Para obtener más información sobre estas funciones, vea [Funciones FILESTREAM y FileTable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql).  
  
-   Todo acceso a los datos de FILESTREAM o FileTable a través de las API del sistema de archivos debe utilizar VNN en lugar de nombres de equipo. Para obtener más información, vea [FILESTREAM y FileTable con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Habilitar los requisitos previos de FileTables](enable-the-prerequisites-for-filetable.md)   
 [Crear, modificar y quitar FileTables](create-alter-and-drop-filetables.md)   
 [Obtener acceso a FileTables con Transact-SQL](access-filetables-with-transact-sql.md)   
 [Obtener acceso a FileTables con API de entrada-salida de archivo](access-filetables-with-file-input-output-apis.md)  
  
  
