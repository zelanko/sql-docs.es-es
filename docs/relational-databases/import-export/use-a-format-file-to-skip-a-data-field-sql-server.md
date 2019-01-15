---
title: Usar un archivo de formato para omitir un campo de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82df9a4dc4a7abce935e87e515cf63f71af0e4b7
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256790"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>Usar un archivo de formato para omitir un campo de datos (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Un archivo de datos puede contener más campos que el número de columnas de la tabla. En este tema se describe la modificación de archivos de formato XML y no XML para adaptarse a un archivo de datos con más campos asignando las columnas de la tabla a los campos de datos correspondientes y omitiendo los campos adicionales.  Revise [Crear un archivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para información adicional.

|Esquema|
|---|
|[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de datos de ejemplo](#sample_data_file)<br />[Creación de los archivos de formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Creación de un archivo de formato no XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Modificación de un archivo de formato no XML](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[Creación de un archivo de formato XML](#xml_format_file)<br />&emsp;&#9679;&emsp;[Modificación de un archivo de formato XML](#modify_xml_format_file)<br />[Importación de datos con un archivo de formato para omitir un campo de datos](#import_data)<br />&emsp;&#9679;&emsp;[Uso de bcp y un archivo de formato no XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Uso de bcp y un archivo de formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y un archivo de formato no XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y un archivo de formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y archivo de formato no XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y archivo de formato XML](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
> [!NOTE]
>  Puede usarse un archivo de formato XML o no XML para importar en bloque un archivo de datos en la tabla mediante un comando de la [utilidad bcp](../../tools/bcp-utility.md), una instrucción [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o una instrucción INSERT… SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Para obtener más información, vea [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).

## Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de archivos de formato modificados de este tema se basan en la tabla y archivo de datos definidos a continuación.
  
### Tabla de ejemplo<a name="sample_table"></a>
El script siguiente crea una base de datos de prueba y una tabla llamada `myTestSkipField`.  Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
 
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myTestSkipField
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30)
   );
```
  
### Archivo de datos de ejemplo<a name="sample_data_file"></a>
Cree un archivo vacío `D:\BCP\myTestSkipField.bcp` e inserte los datos siguientes: 
```
1,SkipMe,Anthony,Grosse
2,SkipMe,Alica,Fatnowna
3,SkipMe,Stella,Rosenhain
```
  
## Creación de los archivos de formato<a name="create_format_file"></a>
Para realizar una importación masiva de datos de `myTestSkipField.bcp` en la tabla `myTestSkipField` , el archivo de formato debe llevar a cabo lo siguiente:
* Asignar el primer campo de datos a la primera columna, `PersonID`.
* Omitir el segundo campo de datos.
* Asignar el tercer campo de datos a la segunda columna, `FirstName`.
* Asignar el cuarto campo de datos a la tercera columna, `LastName`.  

Se trata del método más sencillo para crear el archivo de formato mediante la [utilidad bcp](../../tools/bcp-utility.md).  En primer lugar, cree un archivo de formato base a partir de la tabla existente.  En segundo lugar, modifique el archivo de formato base para reflejar el archivo de datos real.
  
### <a name="nonxml_format_file"></a>Creación de un archivo de formato no XML 
Revise [Archivos de formato no XML [SQL Server]](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para información detallada. El siguiente comando hará uso de la [utilidad bcp](../../tools/bcp-utility.md) para generar un archivo de formato no XML, `myTestSkipField.fmt`, basado en el esquema de `myTestSkipField`.  Además, el calificador `c` se usa para especificar los datos de caracteres, `t,` se usa para especificar una coma como terminador de campo y `T` se usa para especificar una conexión de confianza que usa seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -f D:\BCP\myTestSkipField.fmt -t, -T
```

### Modificación del archivo de formato no XML <a name="modify_nonxml_format_file"></a>
Consulte [Estructura de los archivos de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) para terminología. Abra `D:\BCP\myTestSkipField.fmt` en el Bloc de notas y realice las modificaciones siguientes:
1) Copie toda la fila del archivo de formato para `FirstName` y péguela directamente después de `FirstName` en la línea siguiente.
2) Aumente el valor del pedido del campo de archivo de host en 1 para la fila nueva y todas las filas subsiguientes.
3) Aumente el valor del número de columnas para reflejar el número real de campos en el archivo de datos.
3) Modifique el orden de la columna del servidor de `2` a `0` en la segunda fila del archivo de formato. 

Compare los cambios realizados:  
**Antes del**
```
13.0
3
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS
```
**Después**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID     ""
2       SQLCHAR 0       25      ","      0     FirstName    SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName    SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       50      "\r\n"   3     LastName     SQL_Latin1_General_CP1_CI_AS

```

El archivo de formato modificado ahora refleja:
* 4 campos de datos
* El primer campo de datos de `myTestSkipField.bcp` está asignado a la primera columna, ` myTestSkipField.. PersonID`
* El segundo campo de datos de `myTestSkipField.bcp` no está asignado a ninguna columna.
* El tercer campo de datos de `myTestSkipField.bcp` está asignado a la segunda columna, `myTestSkipField.. FirstName`
* El cuarto campo de datos de `myTestSkipField.bcp` está asignado a la tercera columna. `myTestSkipField.. LastName`

### Creación de un archivo de formato XML <a name="xml_format_file"></a>  
Revise [Archivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para información detallada.  El siguiente comando hará uso de la [utilidad bcp](../../tools/bcp-utility.md) para crear un archivo de formato xml, `myTestSkipField.xml`, basado en el esquema de `myTestSkipField`.  Además, el calificador `c` se usa para especificar los datos de caracteres, `t,` se usa para especificar una coma como terminador de campo y `T` se usa para especificar una conexión de confianza que usa seguridad integrada.  El calificador `x` se debe usar para generar un archivo de formato basado en XML.  En el símbolo del sistema, escriba el siguiente comando:

```
bcp TestDatabase.dbo.myTestSkipField format nul -c -x -f D:\BCP\myTestSkipField.xml -t, -T
```

### Modificación del archivo de formato XML <a name="modify_xml_format_file"></a>
Consulte [Sintaxis de esquema para archivos de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) para terminología.  Abra `D:\BCP\myTestSkipField.xml` en el Bloc de notas y realice las modificaciones siguientes:
1) Copie todo el segundo campo y péguelo directamente después del segundo campo en la línea siguiente.
2) Aumente el valor "FIELD ID" en 1 para el nuevo campo FIELD y cada campo FIELD subsiguiente.
3) Aumente el valor de "COLUMN SOURCE" en 1 para `FirstName`y `LastName` para reflejar la asignación revisada.

Compare los cambios realizados:  
**Antes del**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

**Después**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLVARYCHAR"/>
 </ROW>
</BCPFORMAT>
```

El archivo de formato modificado ahora refleja:
* 4 campos de datos
* FIELD 1, que corresponde a COLUMN 1, se asigna a la primera columna de tabla, `myTestSkipField.. PersonID`
* FIELD 2 no corresponde a ninguna COLUMN y, por lo tanto, se asigna a ninguna columna de tabla.
* FIELD 3, que corresponde a COLUMN 3, se asigna a la segunda columna de tabla, `myTestSkipField.. FirstName`
* FIELD 4, que corresponde a COLUMN 4, se asigna a la tercera columna de tabla, `myTestSkipField.. LastName`

## Importación de datos con un archivo de formato para omitir un campo de datos<a name="import_data"></a>
Los ejemplos siguientes usan la base de datos, el archivo de datos y los archivos de formato que se han creado anteriormente.

### Uso de [bcp](../../tools/bcp-utility.md) y un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.fmt -T
```

### Uso de [bcp](../../tools/bcp-utility.md) y un [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myTestSkipField IN D:\BCP\myTestSkipField.bcp -f D:\BCP\myTestSkipField.xml -T
```

### Uso de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Uso de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y un [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
BULK INSERT dbo.myTestSkipField   
   FROM 'D:\BCP\myTestSkipField.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myTestSkipField.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Uso de [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a>    
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

### Uso de [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myTestSkipField;
INSERT INTO dbo.myTestSkipField 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myTestSkipField.bcp',
        FORMATFILE = 'D:\BCP\myTestSkipField.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myTestSkipField;
```

  
## <a name="see-also"></a>Consulte también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
