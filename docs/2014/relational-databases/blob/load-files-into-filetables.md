---
title: Carga de archivos en FileTables | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 04f32e1f1d0bc67e567a2a4d30779f13af6c68a6
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536040"
---
# <a name="load-files-into-filetables"></a>Cargar archivos en FileTables
  Describe cómo se cargan o migran archivos en las FileTables.  
  
##  <a name="BasicsLoadNew"></a> Cargar o migrar archivos en una FileTable  
 El método que elija para cargar o migrar archivos en una FileTable dependerá del lugar en el que estén almacenados actualmente los archivos.  
  
|Ubicación actual de los archivos|Opciones de migración|  
|-------------------------------|---------------------------|  
|Los archivos están almacenados actualmente en el sistema de archivos.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene información de los archivos.|Dado que una FileTable aparece como carpeta en el sistema de archivos de Windows, puede cargar archivos fácilmente en una nueva FileTable mediante cualquiera de los métodos disponibles para mover o copiar archivos. Estos métodos incluyen el Explorador de Windows, las opciones de la línea de comandos (incluidas xcopy y robocopy), así como aplicaciones o scripts personalizados.<br /><br /> No puede convertir una carpeta existente en una FileTable.|  
|Los archivos están almacenados actualmente en el sistema de archivos.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye una tabla de metadatos que contiene punteros a los archivos.|El primer paso es mover o copiar los archivos mediante uno de los métodos mencionados anteriormente.<br /><br /> El segundo paso es actualizar la tabla de metadatos existente para que señale a la nueva ubicación de los archivos.<br /><br /> Para más información, vea [Ejemplo: Migrar archivos desde el sistema de archivos en una FileTable](#HowToMigrateFiles) en este tema.|  
  
###  <a name="HowToLoadNew"></a> Cómo: Cargar archivos en una FileTable  
 Los métodos que puede usar para cargar archivos en una FileTable son:  
  
-   Arrastrar y colocar los archivos desde las carpetas de origen hasta la nueva carpeta de FileTable del Explorador de Windows.  
  
-   Usar opciones de la línea de comando como MOVE, COPY, XCOPY o ROBOCOPY desde el símbolo del sistema o en un archivo o un script por lotes.  
  
-   Escribir una aplicación personalizada en C# o Visual Basic.NET que use los métodos del espacio de nombres **System.IO** para mover o copiar los archivos.  
  
###  <a name="HowToMigrateFiles"></a> Ejemplo: Migrar archivos desde el sistema de archivos en una FileTable  
 En este escenario, los archivos se almacenan en el sistema de archivos y dispone de una tabla de metadatos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene punteros a los archivos. Puede mover los archivos a una FileTable y reemplazar después la ruta de acceso UNC original de cada archivo de los metadatos por la ruta de acceso UNC de la FileTable. La función [GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql) sirve para lograr este propósito.  
  
 Este ejemplo, suponga que hay una tabla de base de datos existente, `PhotoMetadata`, que contiene datos sobre fotografías. Esta tabla tiene una columna `UNCPath` de tipo `varchar`(512) que contienen la ruta de acceso UNC real de un archivo .jpg.  
  
 Debe emprender las siguientes acciones para migrar los archivos de imagen desde el sistema de archivos a una FileTable:  
  
1.  Cree una nueva FileTable para almacenar los archivos. En este ejemplo se usa el nombre de tabla, `dbo.PhotoTable`, pero no se muestra el código para crearla.  
  
2.  Usar xcopy o una herramienta similar para copiar los archivos .jpg, con su estructura de directorio, en el directorio raíz de la FileTable.  
  
3.  Corregir los metadatos de la tabla `PhotoMetadata`, mediante el uso de código parecido al siguiente:  
  
```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="BasicsBulkLoad"></a> Cargar de forma masiva archivos en una FileTable  
 Una FileTable se comporta como una tabla normal en las operaciones masivas, con los requisitos siguientes.  
  
 Una FileTable tiene restricciones definidas por el sistema que garantizan que se mantiene la integridad del espacio de nombres de archivo o de directorio. Estas restricciones deben comprobarse en los datos cargados de forma masiva en la FileTable. Como algunas operaciones de inserción masiva permiten omitir las restricciones de tabla, se aplicarán los siguientes requisitos.  
  
-   Las operaciones de carga masiva que aplican restricciones pueden ejecutarse en una FileTable exactamente igual que en cualquier otra tabla. Esta categoría incluye las siguientes operaciones:  
  
    -   bcp con la cláusula CHECK_CONSTRAINTS.  
  
    -   BULK INSERT con la cláusula CHECK_CONSTRAINTS.  
  
    -   INSERT INTO ... SELECT * FROM OPENROWSET(BULK ...) sin la cláusula IGNORE_CONSTRAINTS.  
  
-   Las operaciones de carga masiva que no aplican restricciones no se ejecutarán correctamente a menos que se deshabiliten las restricciones definidas por el sistema para la FileTable. Esta categoría incluye las siguientes operaciones:  
  
    -   bcp sin la cláusula CHECK_CONSTRAINTS.  
  
    -   BULK INSERT sin la cláusula CHECK_CONSTRAINTS.  
  
    -   INSERT INTO ... SELECT * FROM OPENROWSET(BULK ...) con la cláusula IGNORE_CONSTRAINTS.  
  
###  <a name="HowToBulkLoad"></a> Cómo: Archivos de carga masiva en una FileTable  
 Puede usar varios métodos para cargar de forma masiva archivos en una FileTable:  
  
-   **bcp**  
  
    -   Se llama con la cláusula **CHECK_CONSTRAINTS** .  
  
    -   Se deshabilita el espacio de nombres de FileTable y se llama sin la cláusula **CHECK_CONSTRAINTS** . A continuación, se vuelve a habilitar el espacio de nombres de la FileTable.  
  
-   **BULK INSERT**  
  
    -   Se llama con la cláusula **CHECK_CONSTRAINTS** .  
  
    -   Se deshabilita el espacio de nombres de FileTable y se llama sin la cláusula **CHECK_CONSTRAINTS** . A continuación, se vuelve a habilitar el espacio de nombres de la FileTable.  
  
-   **INSERT INTO ... SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   Se llama con la cláusula **IGNORE_CONSTRAINTS** .  
  
    -   Se deshabilita el espacio de nombres de FileTable y se llama sin la cláusula **IGNORE_CONSTRAINTS** . A continuación, se vuelve a habilitar el espacio de nombres de la FileTable.  
  
 Para obtener más información sobre cómo deshabilitar las restricciones de FileTable, vea [Administrar FileTables](manage-filetables.md).  
  
###  <a name="disabling"></a> Cómo: Deshabilitar restricciones de FileTable para carga masiva  
 Para realizar la carga masiva de datos en una FileTable sin la sobrecarga que supone la aplicación de restricciones definidas por el sistema, puede deshabilitar temporalmente estas restricciones. Para obtener más información, vea [Administrar FileTables](manage-filetables.md).  
  
## <a name="see-also"></a>Vea también  
 [Obtener acceso a FileTables con Transact-SQL](access-filetables-with-transact-sql.md)   
 [Obtener acceso a FileTables con API de entrada-salida de archivo](access-filetables-with-file-input-output-apis.md)  
  
  
