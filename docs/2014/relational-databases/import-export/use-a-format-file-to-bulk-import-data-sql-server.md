---
title: Usar un archivo de formato para importar datos en bloque (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f46357975476ac301c28f639a3508edc992e5e5b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112690"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Usar un archivo de formato para importar datos de forma masiva (SQL Server)
  En este tema se describe cómo usar un archivo de formato en operaciones de importación masiva. El archivo de formato asigna los campos del archivo de datos a las columnas de la tabla.  Puede usar un archivo de formato XML o no XML para importar datos en bloque al usar un comando **bcp** o un comando BULK INSERT o INSERT ... SELECT * FROM OPENROWSET(BULK...) de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Para que un archivo de formato trabaje con un archivo de datos de caracteres Unicode, todos los campos de entrada deben ser cadenas de texto Unicode (es decir, de tamaño fijo o cadenas Unicode terminadas en caracteres).  
  
> [!NOTE]  
>  Si no está familiarizado con los archivos de formato, vea [archivos de formato no XML &#40;SQL Server&#41; ](xml-format-files-sql-server.md) y [archivos de formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="format-file-options-for-bulk-import-commands"></a>Opciones de los archivos de formato para los comandos de importación masiva  
 La siguiente tabla resume la opción de archivo de formato para cada uno de los comandos de importación masiva.  
  
|Comando de carga masiva|Opción de archivo de formato|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|FORMATFILE = '*format_file_path*'|  
|**bcp** … **in**|**-f** *format_file*|  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) u [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Para importar o exportar datos SQLXML de manera masiva, use uno de los siguientes tipos de datos en el archivo de formato: SQLCHAR o SQLVARYCHAR (los datos se envían en la página de códigos del cliente o en la página de códigos implícita en la intercalación), SQLNCHAR o SQLNVARCHAR (los datos se envían como Unicode), o SQLBINARY o SQLVARYBIN (los datos se envían sin ninguna conversión).  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos de esta sección se muestra cómo usar los archivos de formato para importar datos en bloque mediante el comando **bcp** y las instrucciones BULK INSERT e INSERT ... SELECT * FROM OPENROWSET(BULK...). Para poder ejecutar los ejemplos de importación masiva, debe crear una tabla, un archivo de datos y un archivo de formato de ejemplo.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren la creación de una tabla denominada **myTestFormatFiles** en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] , bajo el esquema **dbo** . Para crear esta tabla, en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>Archivo de datos de ejemplo  
 Los ejemplos utilizan un archivo de datos de ejemplo, `myTestFormatFiles-c.Dat`, que contiene los siguientes registros. Para crear el archivo de datos, en el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, escriba:  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>Archivos de formato de ejemplo  
 Algunos ejemplos de esta sección utilizan un archivo de formato XML, `myTestFormatFiles-f-x-c.Xml`, mientras que otros ejemplos utilizan un archivo sin formato XML. Ambos archivos de formato usan formatos de datos de caracteres y un terminador de campo que no es el predeterminado (,).  
  
#### <a name="the-sample-non-xml-format-file"></a>Archivo de formato no XML de ejemplo  
 En el siguiente ejemplo se usa **bcp** para generar un archivo de formato XML a partir de la tabla `myTestFormatFiles` . El archivo `myTestFormatFiles.Fmt` incluye la siguiente información:  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 Para usar **bcp** con la opción **format** para crear este archivo de formato, en el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 Para obtener más información sobre cómo crear un archivo de formato, vea [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
#### <a name="the-sample-xml-format-file"></a>Archivo de formato XML de ejemplo  
 En el siguiente ejemplo se usa **bcp** para generar un archivo de formato XML a partir de la tabla `myTestFormatFiles` . El archivo `myTestFormatFiles.Xml` incluye la siguiente información:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 Para usar **bcp** con la opción **format** para crear este archivo de formato, en el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>Usar bcp  
 En el siguiente ejemplo se usa **bcp** para importar datos en bloque desde el archivo de datos `myTestFormatFiles-c.Dat` a la tabla `HumanResources.myTestFormatFiles` en la base de datos de ejemplo. Este ejemplo utiliza un archivo de formato XML, `MyTestFormatFiles.Xml`. El ejemplo elimina todas las filas existentes en la tabla antes de importar el archivo de datos.  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  Para obtener más información sobre este comando, vea [bcp (utilidad)](../../tools/bcp-utility.md).  
  
### <a name="using-bulk-insert"></a>Usar BULK INSERT  
 El siguiente ejemplo usa BULK INSERT para importar datos de forma masiva desde el archivo de datos `myTestFormatFiles-c.Dat` a la tabla `HumanResources.myTestFormatFiles` de la base de datos de ejemplo  [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. Este ejemplo utiliza un archivo sin formato XML, `MyTestFormatFiles.Fmt`. El ejemplo elimina todas las filas existentes en la tabla antes de importar el archivo de datos.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  Para obtener más información sobre esta instrucción, vea [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>Usar el proveedor de conjunto de filas BULK OPENROWSET  
 El siguiente ejemplo usa `INSERT ... SELECT * FROM OPENROWSET(BULK...)` para importar datos de forma masiva desde el archivo de datos `myTestFormatFiles-c.Dat` a la tabla `HumanResources.myTestFormatFiles` de la base de datos de ejemplo de `AdventureWorks` . Este ejemplo utiliza un archivo de formato XML, `MyTestFormatFiles.Xml`. El ejemplo elimina todas las filas existentes en la tabla antes de importar el archivo de datos.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 Cuando haya terminado de utilizar la tabla de ejemplo, puede eliminarse con la siguiente instrucción:  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  Para obtener más información sobre la cláusula OPENROWSET BULK, vea [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
## <a name="additional-examples"></a>Otros ejemplos  
 [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
 [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [XML, archivos de formato &#40;SQL Server&#41;](xml-format-files-sql-server.md)  
  
  
