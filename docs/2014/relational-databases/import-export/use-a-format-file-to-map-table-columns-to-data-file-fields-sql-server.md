---
title: Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos (SQL Server) | Microsoft Docs
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
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f6afe2f0125b7f62f3b4a2b8f00bfba50a883442
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111786"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos (SQL Server)
  Un archivo de datos puede contener campos organizados en un orden diferente al de las columnas correspondientes en la tabla. Este tema trata los archivos de formato XML y no XML que se han modificado para alojar un archivo de datos cuyos campos están organizados en un orden diferente al de las columnas de la tabla. El archivo de formato modificado asigna los campos de datos a las columnas correspondientes de la tabla.  
  
> [!NOTE]  
>  Se puede usar un archivo de formato XML o no XML para realizar una importación en bloque de un archivo de datos en la tabla mediante un comando de **bcp**, la instrucción BULK INSERT o INSERT... SELECT * FROM OPENROWSET(BULK...). Para obtener más información, vea [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md).  
  
## <a name="sample-table-and-data-file"></a>Tabla y archivo de datos de ejemplo  
 Los ejemplos de archivos de formato modificados de este tema se basan en la siguiente tabla y archivo de datos.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos de este tema requieren la creación de una tabla denominada `myTestOrder` en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] , bajo el esquema `dbo` . Para crear esta tabla, en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , ejecute el código siguiente:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>Archivo de datos  
 El archivo de datos, `myTestOrder-c.txt`, contiene los siguientes registros:  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 Para importar masivamente datos desde `myTestSkipCol2-c.dat` a la tabla `myTestSkipCol`, el archivo de formato debe asignar el primer campo de datos a `Col3`, el segundo campo de datos a `Col2`, el tercer campo de datos a `Col1` y el cuarto campo de datos a `Col4`.  
  
## <a name="using-a-non-xml-format-file"></a>Usar un archivo de formato no XML  
 Puede cambiar el orden de asignación de una columna cambiando el valor de orden de la columna para indicar la posición del campo de datos correspondiente.  
  
 El siguiente archivo de formato no XML de ejemplo presenta un archivo de formato, `myTestOrder.fmt`, que asigna los campos de `myTestOrder-c.txt` a las columnas de la tabla `myTestOrder`. Para obtener información acerca de cómo crear el archivo de datos y la tabla, vea "Tabla y archivo de datos de ejemplo", anteriormente en este tema. El archivo de formato utiliza el formato de datos de carácter.  
  
 El archivo de formato contiene la siguiente información:  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  Para obtener más información sobre el diseño de los archivos de formato no XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo utiliza una instrucción `BULK INSERT` para realizar una importación masiva de datos del archivo de datos `myTestOrder-c.txt` a la tabla de ejemplo `myTestOrder` utilizando el archivo de formato no XML `myTestOrder.fmt`.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>Usar un archivo de formato XML  
 El siguiente archivo de formato no XML de ejemplo muestra un archivo de formato, `myTestOrder.xml`, que asigna los campos de `myTestOrder-c.txt` a las columnas de la tabla `myTestOrder`. Para obtener información sobre la creación del archivo y de la tabla de datos, vea "Tabla y archivo de datos de ejemplo", anteriormente en este tema.  
  
 El archivo de formato `myTestOrder.xml` contiene la siguiente información:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  Para obtener más información sobre la sintaxis del esquema XML y ejemplos adicionales de archivos de formato XML, vea [XML, archivos de formato &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="example"></a>Ejemplo  
 El siguiente ejemplo utiliza el proveedor de conjuntos de filas BULK `OPENROWSET` para importar datos del archivo de datos `myTestOrder-c.txt` a la tabla de ejemplo `myTestOrder` utilizando el archivo de formato XML `myTestOrder.xml` . La instrucción `INSERT… SELECT` especifica la lista de columnas en la lista de selección.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute el siguiente código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  