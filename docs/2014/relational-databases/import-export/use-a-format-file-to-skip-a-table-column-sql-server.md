---
title: Usar un archivo de formato para omitir una columna de tabla (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bc1101225eae5fd02eec2ee7c29e8ca21a778370
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188225"
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>Usar un archivo de formato para omitir una columna de tabla  (SQL Server)
  En este tema se describen los archivos de formato. Se puede utilizar un archivo de formato para omitir la importación de una columna de tabla cuando el campo no existe en el archivo de datos. Un archivo de datos solo puede contener menos campos que el número de columnas en la tabla si las columnas omitidas tienen un valor nulo y/o contienen un valor predeterminado.  
  
## <a name="sample-table-and-data-file"></a>Tabla y archivo de datos de ejemplo  
 Los siguientes ejemplos requieren una tabla denominada `myTestSkipCol` en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] bajo el esquema **dbo** . Para crear esta tabla, realice lo siguiente:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
 En los siguientes ejemplos se utiliza un archivo de datos de ejemplo, `myTestSkipCol2.dat`, que solo contiene dos campos, aunque la tabla correspondiente contiene tres columnas:  
  
```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
  
```  
  
 Para realizar importaciones masivas de datos desde `myTestSkipCol2.dat` en la tabla `myTestSkipCol` , el archivo de formato debe asignar el primer campo de datos a `Col1`, el segundo campo a `Col3`, omitiendo `Col2`.  
  
## <a name="using-a-non-xml-format-file"></a>Usar un archivo de formato no XML  
 Puede modificar un archivo de formato no XML para omitir una columna de tabla. Normalmente, esto implica el uso de la utilidad **bcp** para crear un archivo de formato no XML predeterminado y la modificación del archivo predeterminado en un editor de texto. El archivo de formato modificado debe asignar cada uno de los campos existentes a su columna de tabla correspondiente e indicar las columnas que se deben omitir. Para modificar un archivo de datos de formato no XML predeterminado existen dos alternativas. Cada alternativa indica que el campo de datos no existe en el archivo de datos y que no se insertará ningún dato en la columna correspondiente de la tabla.  
  
### <a name="creating-a-default-non-xml-format-file"></a>Crear un archivo de formato no XML predeterminado  
 En este tema se usa el archivo de formato no XML predeterminado que se creó para la tabla de ejemplo `myTestSkipCol` mediante el siguiente comando **bcp** :  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  
  
 En el ejemplo anterior se crea un archivo de formato no XML, `myTestSkipCol_Default.fmt`. Este formato de archivo se denomina *archivo de formato predeterminado* porque es el formulario generado por **bcp**. Normalmente, un archivo de formato predeterminado describe una correspondencia uno a uno entre los campos de archivo de datos y las columnas de la tabla.  
  
> [!IMPORTANT]  
>  Es posible que deba especificar el nombre de la instancia de servidor a la que se va a conectar. También es posible que deba especificar el nombre de usuario y la contraseña. Para más información, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
 En la siguiente ilustración se muestran los valores de estos archivos de formato predeterminados de ejemplo. La ilustración también muestra el nombre de cada campo de archivo de formato.  
  
 ![archivo de formato no XML predeterminado para myTestSkipCol](../../database-engine/media/mytestskipcol-f-c-default-fmt.gif "archivo de formato no XML predeterminado para myTestSkipCol")  
  
> [!NOTE]  
>  Para obtener más información sobre los campos de archivo de formato, vea [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="methods-for-modifying-a-non-xml-format-file"></a>Métodos para modificar un archivo de formato no XML  
 Para omitir una columna de tabla, edite el archivo de formato no XML predeterminado y modifíquelo utilizando uno de los siguientes métodos alternativos:  
  
-   El método preferido consta de tres pasos básicos. Primero, elimine cualquier fila de archivo de formato que describa un campo que no esté en el archivo de datos. A continuación, reduzca el valor "Orden de campo del archivo host" de cada fila de archivo de formato antecedida por una fila eliminada. El objetivo es tener valores "Orden de campo del archivo host" secuenciales, de 1 a *n*, que reflejen la posición real de cada campo de datos del archivo de datos. Por último, reduzca el valor del campo "Número de columnas" para que se ajuste al número real de campos del archivo de datos.  
  
     El ejemplo siguiente se basa en el archivo de formato predeterminado para la tabla `myTestSkipCol` , que se creó en "Crear un archivo de formato no XML predeterminado", anteriormente en este tema. Este archivo de formato modificado asigna el primer campo de datos a `Col1`, omite `Col2`y asigna el segundo campo de datos a `Col3`. La fila para `Col2` se ha eliminado. Otras modificaciones se indican en negrita:   
  
    ```  
    9.0  
    2  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
-   Como alternativa, para omitir una columna de tabla, puede modificar la definición de la fila de archivo de formato que corresponda a la columna de tabla. En esta fila de formato de archivo los valores "prefix length", "host file data length" y "server column order" deben estar configurados en 0. Además, los campos "terminator" y "column collation" deben estar establecidos en "" (NULL).  
  
     El valor "nombre de columna de servidor" requiere una cadena que no esté en blanco, aunque el nombre de columna real no es necesario. Los campos de formato restantes requieren los valores predeterminados.  
  
     El siguiente ejemplo también se deriva del archivo de formato predeterminado para la tabla `myTestSkipCol` . Los valores que deben ser 0 o NULL se indican en negrita.  
  
    ```  
    9.0  
    3  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       00""0     Col2         ""  
    3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
### <a name="examples"></a>Ejemplos  
 Los siguientes ejemplos también se basan en la tabla de ejemplo `myTestSkipCol` y el archivo de datos de ejemplo `myTestSkipCol2.dat` que se crearon en "Tabla y archivo de datos de ejemplo" anteriormente en este tema.  
  
#### <a name="using-bulk-insert"></a>Usar BULK INSERT  
 Este ejemplo funciona con cualquiera de los archivos de formato no XML modificados que se crearon en "Métodos para modificar un archivo de formato no XML" anteriormente en este tema. En este ejemplo, el archivo de formato modificado se llama `C:\myTestSkipCol2.fmt`. Para usar `BULK INSERT` a fin de importar de forma masiva el archivo de datos `myTestSkipCol2.dat` , en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute el siguiente código:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="using-an-xml-format-file"></a>Usar un archivo de formato XML  
 Con un archivo de formato XML, no se puede omitir una columna cuando se importa directamente a una tabla mediante el comando **bcp** o una instrucción BULK INSERT. Sin embargo, se puede importar en todas las columnas de una tabla, excepto en la última columna. Si se tienen que omitir todas las columnas excepto la última, se debe crear una vista de la tabla de destino que contenga únicamente las columnas incluidas en el archivo de datos. De esta forma, se puede realizar una importación masiva de los datos de ese archivo en la vista.  
  
 Para utilizar un archivo de formato XML para omitir una columna de la tabla mediante OPENROWSET(BULK...), debe proporcionar una lista explícita de las columnas en la lista de selección y en la tabla de destino de la siguiente manera:  
  
 INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)  
  
### <a name="creating-a-default-xml-format-file"></a>Crear un archivo de formato XML predeterminado  
 Los ejemplos de archivos de formato modificado se basan en la tabla `myTestSkipCol` y el archivo de datos de ejemplo que se crearon en "Tabla y archivo de datos de ejemplo" anteriormente en este tema. El siguiente comando **bcp** crea un archivo de formato XML predeterminado para la tabla `myTestSkipCol` :  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
 El archivo de formato no XML predeterminado resultante describe una correspondencia uno a uno entre los archivos de campos de datos y las columnas de la tabla, de esta forma:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Para obtener más información sobre la estructura de los archivos de formato XML, vea [XML, archivos de formato &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Ejemplos  
 Los ejemplos de esta sección utilizan la tabla de ejemplo `myTestSkipCol` y el archivo de datos de ejemplo `myTestSkipCol2.dat` que se crearon en "Tabla de ejemplo y archivo de datos" anteriormente en este tema. Para importar datos desde `myTestSkipCol2.dat` a la tabla `myTestSkipCol` , los ejemplos utilizan el siguiente archivo de formato XML modificado, `myTestSkipCol2-x.xml`. Esto se basa en el archivo de formato que se creó en "Crear un archivo de formato XML predeterminado", anteriormente en este tema.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
#### <a name="using-openrowsetbulk"></a>Usar OPENROWSET(BULK...)  
 En el siguiente ejemplo se utiliza el proveedor de conjuntos de filas BULK `OPENROWSET` y el archivo de formato `myTestSkipCol2.xml` . En el ejemplo se importa masivamente el archivo de datos `myTestSkipCol2.dat` a la tabla `myTestSkipCol` . La instrucción contiene una lista explícita de las columnas en la lista de selección y también en la tabla de destino, según convenga.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute el siguiente código:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```  
  
#### <a name="using-bulk-import-on-a-view"></a>Utilizar BULK IMPORT en una vista  
 En el siguiente ejemplo se crea `v_myTestSkipCol` en la tabla `myTestSkipCol` . Esta vista omite la segunda columna de la tabla, `Col2`. Después, en el ejemplo se usa `BULK INSERT` para importar el archivo de datos `myTestSkipCol2.dat` a la vista.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute el siguiente código:  
  
```  
CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
USE AdventureWorks2012;  
GO  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
