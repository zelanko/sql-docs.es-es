---
title: Obtener acceso a FileTables con Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: filestream
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 005861d35a9e89c59ac7e0311f41a90caee37f8e
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2018
ms.locfileid: "36772230"
---
# <a name="access-filetables-with-transact-sql"></a>Obtener acceso a FileTables con Transact-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Describe el funcionamiento de los comandos del lenguaje de manipulación de datos (DML) de [!INCLUDE[tsql](../../includes/tsql-md.md)] con FileTables.  
  
##  <a name="BasicsInsert"></a> Operaciones INSERT en FileTables  
 Las consideraciones siguientes se aplican a las operaciones **INSERT** en FileTables:  
  
-   Todas las columnas de atributos de archivo tienen restricciones NOT NULL. Si los valores no se establecen de forma explícita, se proporcionan los valores predeterminados adecuados.  
  
-   Se aplican las restricciones definidas por el sistema si la instrucción INSERT establece los atributos **name**, **path_locator**, **parent_path_locator** o file.  
  
-   La aplicación puede obtener el valor de **path_locator** de un archivo o un directorio si proporciona la ruta de acceso al sistema de archivos a la función [GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md).  
  
##  <a name="BasicsUpdate"></a> Operaciones UPDATE en FileTables  
 Las consideraciones siguientes se aplican a las operaciones **UPDATE** en FileTables:  
  
-   Se permiten actualizaciones en los datos definidos por el usuario.  
  
-   Se aplican las restricciones definidas por el sistema si la instrucción INSERT establece los atributos **name**, **path_locator**, **parent_path_locator**o file.  
  
-   Las actualizaciones pueden realizarse en los datos FILESTREAM de la columna **file_stream** sin que se vea afectada ninguna de las demás columnas, incluidas las marcas de tiempo.  
  
##  <a name="BasicsDelete"></a> Operaciones DELETE en FileTables  
 Las consideraciones siguientes se aplican a las operaciones **DELETE** en FileTables:  
  
-   Al eliminar una fila, también se quita el archivo o directorio correspondiente del sistema de archivos.  
  
-   Al eliminar una fila se produce un error si la fila corresponde a un directorio que contiene otros archivos o directorios.  
  
##  <a name="BasicsConstraints"></a> Restricciones que se aplican a operaciones DML en FileTables  
 Las restricciones definidas por el sistema garantizan que las acciones DML no comprometan la integridad de la jerarquía del espacio de nombres de archivo. Las restricciones que se aplican incluyen las siguientes:  
  
-   Al establecer o cambiar el **nombre** del archivo o del directorio:  
  
    -   Se aplican las convenciones de nomenclatura de archivos y directorios de Windows.  
  
    -   Se aplica la unicidad de nombres en el directorio primario.  
  
-   Al establecer o cambiar la ubicación de un archivo o un directorio mediante el establecimiento o el cambio de **path_locator** o **parent_path_locator**:  
  
    -   Se aplica la unicidad.  
  
    -   Se aplica la coherencia del árbol jerárquico de directorios y archivos, incluida la coherencia de los valores de **path_locator** y **parent_path_locator** .  
  
-   El valor de **is_directory** no se puede establecer en true cuando la columna **file_stream** no es NULL. Los datos de la columna **file_stream** indican que la fila representa un archivo y no un directorio.  
  
-   Las columnas de atributos de archivo no pueden ser NULL. Las restricciones NOT NULL se aplican con valores predeterminados.  
  
-   El valor de **last_access_time** no puede ser anterior a **last_write_time** y **creation_time**.  
  
## <a name="see-also"></a>Ver también  
 [Cargar archivos en FileTables](../../relational-databases/blob/load-files-into-filetables.md)   
 [Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Obtener acceso a FileTables con API de entrada-salida de archivo](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [DDL de FileTable, funciones, procedimientos almacenados y vistas](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
