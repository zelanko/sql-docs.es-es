---
title: Obtener acceso a datos FILESTREAM con Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Transact-SQL
ms.assetid: a6bf0ce7-7e5e-4a07-8917-ee526c9d0a05
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 067f14e857addc5f43a0b17d81d554997adbc09f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010443"
---
# <a name="access-filestream-data-with-transact-sql"></a>Obtener acceso a datos FILESTREAM con Transact-SQL
  En este tema se describe cómo utilizar las instrucciones INSERT, DELETE y UPDATE de [!INCLUDE[tsql](../../includes/tsql-md.md)] para administrar los datos de FILESTREAM.  
  
> [!NOTE]  
>  Los ejemplos de este tema requieren la tabla y la base de datos habilitada para FILESTREAM que se crean en [Crear una base de datos habilitada para FILESTREAM](create-a-filestream-enabled-database.md) y [Crear una tabla para almacenar datos FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
##  <a name="ins"></a> Insertar una fila que contiene datos FILESTREAM  
 Para agregar una fila a una tabla que admite datos FILESTREAM, use la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT. Al insertar datos en una columna FILESTREAM, se puede insertar NULL o un valor `varbinary(max)`.  
  
### <a name="inserting-null"></a>Insertar NULL  
 El ejemplo siguiente muestra la forma de utilizar el valor `NULL`. Cuando el valor FILESTREAM es `NULL`, [!INCLUDE[ssDE](../../includes/ssde-md.md)] no crea un archivo en el sistema de archivos.  
  
 [!code-sql[FILESTREAM#FS_InsertNULL](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertnull)]  
  
### <a name="inserting-a-zero-length-record"></a>Insertar un registro de longitud cero  
 En el siguiente ejemplo se muestra cómo utilizar `INSERT` para crear un registro de longitud cero. Esto es útil cuando se desea obtener un identificador de archivo, pero el archivo se va a tratar con las API de Win32.  
  
 [!code-sql[FILESTREAM#FS_InsertZero](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertzero)]  
  
### <a name="creating-a-data-file"></a>Crear un archivo de datos  
 En el siguiente ejemplo se muestra cómo utilizar `INSERT` para crear un archivo que contiene datos. [!INCLUDE[ssDE](../../includes/ssde-md.md)] convierte la cadena `Seismic Data` en un valor `varbinary(max)` . FILESTREAM crea el archivo de Windows si aún no existe. A continuación, los datos se agregan al archivo de datos.  
  
 [!code-sql[FILESTREAM#FS_InsertData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_insertdata)]  
  
 Cuando selecciona todos los datos de la tabla `Archive`.`dbo.Records` , los resultados son similares a los que se muestran en la tabla siguiente. Sin embargo, la columna `Id` contendrá GUID diferentes.  
  
|Identificador|SerialNumber|Reanudar|  
|--------|------------------|------------|  
|`C871B90F-D25E-47B3-A560-7CC0CA405DAC`|`1`|`NULL`|  
|`F8F5C314-0559-4927-8FA9-1535EE0BDF50`|`2`|`0x`|  
|`7F680840-B7A4-45D4-8CD5-527C44D35B3F`|`3`|`0x536569736D69632044617461`|  
  
##  <a name="upd"></a> Actualizar datos FILESTREAM  
 Puede usar [!INCLUDE[tsql](../../includes/tsql-md.md)] para actualizar los datos del archivo del sistema de archivos; sin embargo, puede no ser conveniente si hay que transmitir grandes cantidades de datos a un archivo.  
  
 En el ejemplo siguiente se reemplaza cualquier texto del registro del archivo por el texto `Xray 1`.  
  
 [!code-sql[FILESTREAM#FS_UpdateData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_updatedata)]  
  
##  <a name="del"></a> Eliminar datos FILESTREAM  
 Al eliminar una fila que contiene un campo FILESTREAM, también elimina sus archivos de sistema de archivos subyacentes. La única manera de eliminar una fila y por consiguiente el archivo, es utilizar la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] DELETE.  
  
 El ejemplo siguiente muestra cómo eliminar una fila y sus archivos de sistema de archivo asociados.  
  
 [!code-sql[FILESTREAM#FS_DeleteData](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_deletedata)]  
  
 Al seleccionar todos los datos de la tabla `dbo.Archive` , la fila ya no está. Ya no puede utilizar el archivo asociado.  
  
> [!NOTE]  
>  El recolector de elementos no utilizados de FILESTREAM quita los archivos subyacentes.  
  
## <a name="see-also"></a>Vea también  
 [Habilitar y configurar FILESTREAM](enable-and-configure-filestream.md)   
 [Evitar conflictos con operaciones de base de datos en aplicaciones FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
