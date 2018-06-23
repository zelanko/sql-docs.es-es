---
title: Usar un archivo de formato para omitir un campo de datos (SQL Server) | Microsoft Docs
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
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a60d4d668cb9c7d7d13a60a12df1057b24eea465
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198693"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>Usar un archivo de formato para omitir un campo de datos (SQL Server)
  Un archivo de datos puede contener más campos que el número de columnas de la tabla. En este tema se describe la modificación de archivos de formato XML y no XML para adaptarse a un archivo de datos con más campos asignando las columnas de la tabla a los campos de datos correspondientes y omitiendo los campos adicionales.  
  
> [!NOTE]  
>  Puede usarse un archivo de formato XML o no XML para importar en bloque un archivo de datos en la tabla mediante un comando **bcp**, una instrucción BULK INSERT o una instrucción INSERT… SELECT * FROM OPENROWSET(BULK...). Para obtener más información, vea [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md).  
  
## <a name="sample-data-file-and-table"></a>Archivo de datos y tabla de ejemplo  
 Los ejemplos de archivos de formato modificados de este tema se basan en la siguiente tabla y archivo de datos.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren la creación de una tabla denominada `myTestSkipField` en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] , bajo el esquema `dbo` . Para crear esta tabla, en el Editor de consultas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , ejecute el código siguiente:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>Archivo de datos de ejemplo  
 El archivo de datos, `myTestSkipField-c.dat`, contiene los siguientes registros:  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 Para realizar una importación masiva de datos de `myTestSkipField-c.dat` en la tabla `myTestSkipField` , el archivo de formato debe llevar a cabo lo siguiente:  
  
-   Asignar el primer campo de datos a la primera columna, `PersonID`.  
  
-   Omitir el segundo campo de datos.  
  
-   Asignar el tercer campo de datos a la segunda columna, `FirstName`.  
  
-   Asignar el cuarto campo de datos a la tercera columna, `LastName`.  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>Archivo de formato no XML para más campos de datos  
 El siguiente archivo de formato, `myTestSkipField.fmt`, asigna los campos de `myTestSkipField-c.dat` a las columnas de la tabla `myTestSkipField`. El archivo de formato utiliza el formato de datos de carácter. Para omitir la asignación de columnas, es necesario cambiar su valor de orden de columna a 0, como se muestra para la columna `ExtraField` del archivo de formato.  
  
 El archivo de formato `myTestSkipField.fmt` contiene la siguiente información:  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  Para obtener más información sobre la sintaxis de los archivos de formato no XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `INSERT ... SELECT * FROM OPENROWSET(BULK...)` , que usa el archivo de formato `myTestSkipField.fmt` . En el ejemplo se importa masivamente el archivo de datos `myTestSkipField-c.dat` a la tabla `myTestSkipField` . Para crear la tabla y el archivo de datos de ejemplo, vea "Tabla y archivo de datos de ejemplo", anteriormente en este tema.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , ejecute el siguiente código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>Archivo de formato XML para más campos de datos  
 El archivo de formato presentado en este ejemplo se basa en otro archivo de formato, `myTestSkipField.xml`, que utiliza el formato de datos de carácter y cuyos campos corresponden exactamente en número y orden a las columnas de la tabla `myTestSkipField`. Para ver el contenido de ese archivo de formato, vea [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
 El siguiente archivo de formato, `myTestSkipField.xml`, asigna los campos de `myTestSkipField-c.dat` a las columnas de la tabla `myTestSkipField`. El archivo de formato utiliza el formato de datos de carácter.  
  
 El archivo de formato `myTestSkipField.xml` contiene la siguiente información:  
  
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
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `INSERT ... SELECT * FROM OPENROWSET(BULK...)` , que usa el archivo de formato `myTestSkipField.Xml` . En el ejemplo se importa masivamente el archivo de datos `myTestSkipField-c.dat` a la tabla `myTestSkipField` . Para crear la tabla y el archivo de datos de ejemplo, vea "Tabla y archivo de datos de ejemplo", anteriormente en este tema.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute el siguiente código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  Para obtener más información sobre la sintaxis del esquema XML y ejemplos adicionales de archivos de formato XML, vea [XML, archivos de formato &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
