---
title: Obtener acceso a FileTables con Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4e99d1aa8564c5a69c19c4b8275e0397595d69ea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108980"
---
# <a name="access-filetables-with-transact-sql"></a>Obtener acceso a FileTables con Transact-SQL
  Describe el funcionamiento de los comandos del lenguaje de manipulación de datos (DML) de [!INCLUDE[tsql](../../includes/tsql-md.md)] con FileTables.  
  
##  <a name="BasicsInsert"></a> Operaciones INSERT en FileTables  
 Las consideraciones siguientes se aplican a las operaciones **INSERT** en FileTables:  
  
-   Todas las columnas de atributos de archivo tienen restricciones NOT NULL. Si los valores no se establecen de forma explícita, se proporcionan los valores predeterminados adecuados.  
  
-   Se aplican las restricciones definidas por el sistema si la instrucción INSERT establece los atributos **name**, **path_locator**, **parent_path_locator** o file.  
  
-   La aplicación puede obtener el valor de **path_locator** de un archivo o un directorio si proporciona la ruta de acceso al sistema de archivos a la función [GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Cargar archivos en FileTables](load-files-into-filetables.md)   
 [Trabajar con directorios y rutas de acceso de FileTables](work-with-directories-and-paths-in-filetables.md)   
 [Obtener acceso a FileTables con API de entrada-salida de archivo](access-filetables-with-file-input-output-apis.md)   
 [DDL de FileTable, funciones, procedimientos almacenados y vistas](../views/views.md)  
  
  
