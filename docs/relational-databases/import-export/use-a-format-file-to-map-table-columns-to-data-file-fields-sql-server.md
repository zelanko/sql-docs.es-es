---
title: Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 98b0c3beba33688943bdd767d29b0e9f7f0cefc4
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67579616"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Un archivo de datos puede contener campos organizados en un orden diferente al de las columnas correspondientes en la tabla. Este tema trata los archivos de formato XML y no XML que se han modificado para alojar un archivo de datos cuyos campos están organizados en un orden diferente al de las columnas de la tabla. El archivo de formato modificado asigna los campos de datos a las columnas correspondientes de la tabla.  Revise [Crear un archivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para información adicional.

|Esquema|
|---|
|[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de datos de ejemplo](#sample_data_file)<br />[Creación de los archivos de formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Creación de un archivo de formato no XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Modificación del archivo de formato no XML](#modify_nonxml_format_file)<br />&emsp;&#9679;&emsp;[Creación de un archivo de formato XML](#xml_format_file)<br />&emsp;&#9679;&emsp;[Modificación del archivo de formato XML](#modify_xml_format_file)<br />[Importación de datos con un archivo de formato para asignar columnas de tabla a campos de un archivo de datos](#import_data)<br />&emsp;&#9679;&emsp;[Uso de bcp y un archivo de formato no XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Uso de bcp y un archivo de formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y un archivo de formato no XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y un archivo de formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y archivo de formato no XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y archivo de formato XML](#openrowset_xml)|

> [!NOTE]  
>  Puede usarse un archivo de formato XML o no XML para importar en bloque un archivo de datos en la tabla mediante un comando de la [utilidad bcp](../../tools/bcp-utility.md), una instrucción [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o una instrucción INSERT… SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Para obtener más información, vea [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  

## Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de archivos de formato modificados de este tema se basan en la tabla y archivo de datos definidos a continuación.

### Tabla de ejemplo<a name="sample_table"></a>
El script siguiente crea una base de datos de prueba y una tabla llamada `myRemap`.  Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE myRemap
   (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   Gender char(1)
   );
```

### Archivo de datos de ejemplo<a name="sample_data_file"></a>
Los datos siguientes presentan `FirstName` y `LastName` en el orden inverso según se presentan en la tabla `myRemap`.  Mediante el Bloc de notas, cree un archivo vacío `D:\BCP\myRemap.bcp` e inserte los datos siguientes:
```
1,Grosse,Anthony,M
2,Fatnowna,Alica,F
3,Rosenhain,Stella,F
```

## Creación de los archivos de formato<a name="create_format_file"></a>
Para realizar una importación masiva de datos de `myRemap.bcp` en la tabla `myRemap` , el archivo de formato debe llevar a cabo lo siguiente:
* Asignar el primer campo de datos a la primera columna, `PersonID`.
* Asignar el segundo campo de datos a la tercera columna, `LastName`.
* Asignar el tercer campo de datos a la segunda columna, `FirstName`.
* Asignar el cuarto campo de datos a la cuarta columna, `Gender`.

Se trata del método más sencillo para crear el archivo de formato mediante la [utilidad bcp](../../tools/bcp-utility.md).  En primer lugar, cree un archivo de formato base a partir de la tabla existente.  En segundo lugar, modifique el archivo de formato base para reflejar el archivo de datos real.

### Creación de un archivo de formato no XML<a name="nonxml_format_file"></a>
Revise [Archivos de formato no XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obtener información detallada. El siguiente comando hará uso de la [utilidad bcp](../../tools/bcp-utility.md) para generar un archivo de formato no xml, `myRemap.fmt`, basado en el esquema de `myRemap`.  Además, el calificador `c` se utiliza para especificar los datos de caracteres, `t,` se utiliza para especificar una coma como terminador de campo y `T` se utiliza para especificar una conexión de confianza que usa seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myRemap format nul -c -f D:\BCP\myRemap.fmt -t, -T
```
### Modificación del archivo de formato no XML <a name="modify_nonxml_format_file"></a>
Consulte [Estructura de los archivos de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md#Structure) para terminología.  Abra `D:\BCP\myRemap.fmt` en el Bloc de notas y realice las modificaciones siguientes:
1.  Vuelva a organizar el orden de las filas del archivo de formato para que las filas se encuentren en el mismo orden que los datos de `myRemap.bcp`.
2.  Asegúrese de que los valores del orden del campo del archivo de host son secuenciales.
3.  Asegúrese de que hay un retorno de carro después de la última fila del archivo de formato.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Compare los cambios:     
**Antes del**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID               ""
2       SQLCHAR 0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
**Después**
```
13.0
4
1       SQLCHAR 0       7       ","      1     PersonID               ""
2       SQLCHAR 0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR 0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR 0       1       "\r\n"   4     Gender                 SQL_Latin1_General_CP1_CI_AS

```
El archivo de formato modificado ahora refleja:
* El primer campo de datos de `myRemap.bcp` está asignado a la primera columna, `myRemap.. PersonID`
* El segundo campo de datos de `myRemap.bcp` está asignado a la tercera columna, `myRemap.. LastName`
* El tercer campo de datos de `myRemap.bcp` está asignado a la segunda columna, `myRemap.. FirstName`
* El cuarto campo de datos de `myRemap.bcp` está asignado a la cuarta columna, `myRemap.. Gender`

### Creación de un archivo de formato XML <a name="xml_format_file"></a>  
Revise [Archivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para información detallada.  El siguiente comando hará uso de la [utilidad bcp](../../tools/bcp-utility.md) para crear un archivo de formato xml, `myRemap.xml`, basado en el esquema de `myRemap`.  Además, el calificador `c` se utiliza para especificar los datos de caracteres, `t,` se utiliza para especificar una coma como terminador de campo y `T` se utiliza para especificar una conexión de confianza que usa seguridad integrada.  El calificador `x` se debe usar para generar un archivo de formato basado en XML.  En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myRemap format nul -c -x -f D:\BCP\myRemap.xml -t, -T
```
### Modificación del archivo de formato XML <a name="modify_xml_format_file"></a>
Consulte [Sintaxis de esquema para archivos de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md#StructureOfXmlFFs) para terminología.  Abra `D:\BCP\myRemap.xml` en el Bloc de notas y realice las modificaciones siguientes:
1. El orden en el que se declaran los elementos \<FIELD> en el formato de archivo es el orden en que esos campos aparecen en el archivo de datos, por tanto, invierta el orden de los elementos \<FIELD> con atributos de identificador 2 y 3.
2. Asegúrese de que los valores de atributo de identificador \<FIELD> son secuenciales.
3. El orden de los elementos \<COLUMN> del elemento \<ROW> define el orden en el que la operación masiva los devuelve.  El archivo de formato XML asigna a cada elemento \<COLUMN> un nombre local que no tiene ninguna relación con la columna de la tabla de destino de una operación de importación en bloque.  El orden de los elementos \<COLUMN> es independiente del orden de los elementos \<FIELD> de una definición \<RECORD>.  Cada elemento \<COLUMN> corresponde a un elemento \<FIELD> (cuyo identificador se especifica en el atributo SOURCE del elemento \<COLUMN>).  Por lo tanto, los valores de \<COLUMN> SOURCE son los únicos atributos que requieren revisión.  Invierta el orden de los atributos 2 y 3 de \<COLUMN> SOURCE.

Compare los cambios.  
**Antes del**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
**Después**
```
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="1" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="2" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="Gender" xsi:type="SQLCHAR"/>
 </ROW>
</BCPFORMAT>
```
El archivo de formato modificado ahora refleja:
* FIELD 1, que corresponde a COLUMN 1, se asigna a la primera columna de tabla, `myRemap.. PersonID`
* FIELD 2, que corresponde a COLUMN 2, se reasigna a la tercera columna de tabla, `myRemap.. LastName`
* FIELD 3, que corresponde a COLUMN 3, se reasigna a la segunda columna de tabla, `myRemap.. FirstName`
* FIELD 4, que corresponde a COLUMN 4, se asigna a la cuarta columna de tabla, `myRemap.. Gender`


## Importación de datos con un archivo de formato para asignar columnas de tabla a campos de un archivo de datos<a name="import_data"></a>
Los ejemplos siguientes usan la base de datos, el archivo de datos y los archivos de formato que se han creado anteriormente.

### Uso de [bcp](../../tools/bcp-utility.md) y un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bcp_nonxml"></a>
En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.fmt -T
```

### Uso de [bcp](../../tools/bcp-utility.md) y un [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bcp_xml"></a>
En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myRemap IN D:\BCP\myRemap.bcp -f D:\BCP\myRemap.xml -T
```

### Uso de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="bulk_nonxml"></a>
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Uso de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y un [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="bulk_xml"></a>
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
BULK INSERT dbo.myRemap   
   FROM 'D:\BCP\myRemap.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myRemap.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Uso de [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)<a name="openrowset_nonxml"></a>    
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```

### Uso de [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)<a name="openrowset_xml"></a>
Ejecute el siguiente Transact-SQL en Microsoft SQL Server Management Studio (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myRemap;
INSERT INTO dbo.myRemap 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myRemap.bcp',
        FORMATFILE = 'D:\BCP\myRemap.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myRemap;
```


  
## <a name="see-also"></a>Consulte también  
[bcp Utility](../../tools/bcp-utility.md)   
 [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
