---
title: Usar un archivo de formato para importar datos en bloque (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 4b5116850d429f147bb5bafc51af800e930c3c30
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Usar un archivo de formato para importar datos de forma masiva (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este tema se describe cómo usar un archivo de formato en operaciones de importación masiva.  Un archivo de formato asigna los campos del archivo de datos a las columnas de la tabla.  Revise [Crear un archivo de formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) para información adicional.

|Esquema|
|---|
|[Antes de comenzar](#begin)<br />[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de datos de ejemplo](#sample_data_file)<br />[Creación de los archivos de formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Creación de un archivo de formato no XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Creación de un archivo de formato XML](#xml_format_file)<br />[Usar un archivo de formato para importar datos de forma masiva](#import_data)<br />&emsp;&#9679;&emsp;[Uso de bcp y un archivo de formato no XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Uso de bcp y un archivo de formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y un archivo de formato no XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y un archivo de formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y archivo de formato no XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y archivo de formato XML](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
## Antes de comenzar<a name="begin"></a>
* Para que un archivo de formato trabaje con un archivo de datos de caracteres Unicode, todos los campos de entrada deben ser cadenas de texto Unicode (es decir, de tamaño fijo o cadenas Unicode terminadas en caracteres).
* Para importar o exportar de forma masiva datos [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) , use uno de los tipos de datos siguientes en el archivo de formato:
  * SQLCHAR o SQLVARYCHAR (los datos se envían a la página de códigos del cliente o a la página de códigos implícita por la intercalación).
  * SQLNCHAR o SQLNVARCHAR (los datos se envían como Unicode).
  * SQLBINARY o SQLVARYBIN (los datos se envían sin realizar ninguna conversión).
* Azure SQL Database y Almacenamiento de datos SQL de Azure solo admiten [bcp](../../tools/bcp-utility.md).  Para obtener información adicional, consulte:
  * [Cargar datos en Almacenamiento de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-load/)
  * [Cargar datos de SQL Server en Almacenamiento de datos SQL de Azure (archivos sin formato)](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-from-sql-server-with-bcp/)
  * [Migración de los datos](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-migrate-data/)

## Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de archivos de formato de este tema se basan en la tabla y archivo de datos definidos a continuación.

### **Tabla de ejemplo**<a name="sample_table"></a>
El script siguiente crea una base de datos de prueba y una tabla llamada `myFirstImport`.  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.MyFirstImport (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   BirthDate Date
   );
```

### **Archivo de datos de ejemplo**<a name="sample_data_file"></a>
Mediante el Bloc de notas, cree un archivo vacío `D:\BCP\myFirstImport.bcp` e inserte los datos siguientes:
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

Como alternativa, puede ejecutar el siguiente script de PowerShell para crear y rellenar el archivo de datos:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = Join-Path -Path $dir -ChildPath 'MyFirstImport.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

## Creación de los archivos de formato<a name="create_format_file"></a>
SQL Server admite dos tipos de archivos de formato: XML y no XML.  El formato no XML es el formato original compatible con versiones anteriores de SQL Server.

### **Creación de un archivo de formato no XML**<a name="nonxml_format_file"></a>
Revise [Archivos de formato no XML [SQL Server]](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para información detallada.  El siguiente comando hará uso de la [utilidad BCP](../../tools/bcp-utility.md) para generar un archivo de formato no XML, `myFirstImport.fmt`, basado en el esquema de `myFirstImport`.  Si quiere usar un comando BCP para crear un archivo de formato, especifique el argumento **format** y use **null** en lugar de una ruta de acceso de archivo de datos.  La opción format también requiere la opción **-f** .  Además, en este ejemplo, el calificador **c** se usa para especificar los datos de caracteres, **t,** se usa para especificar una coma como [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)y **T** se usa para especificar una conexión de confianza que usa seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:

```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -f D:\BCP\myFirstImport.fmt -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.fmt
```

El archivo de formato no XML, `D:\BCP\myFirstImport.fmt` debe tener el aspecto siguiente:
```
13.0
4
1       SQLCHAR             0       7       ","      1     PersonID               ""
2       SQLCHAR             0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR             0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR             0       11      "\r\n"   4     BirthDate              ""
```

> [!IMPORTANT]
> Asegúrese de que el archivo de formato no XML termina con un retorno de carro o avance de línea.  De lo contrario, es probable que reciba el mensaje de error siguiente:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

### **Creación de un archivo de formato XML**<a name="xml_format_file"></a>  
Revise [Archivos de formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) para información detallada.  El siguiente comando hará uso de la [utilidad bcp](../../tools/bcp-utility.md) para crear un archivo de formato xml, `myFirstImport.xml`, basado en el esquema de `myFirstImport`. Si quiere usar un comando BCP para crear un archivo de formato, especifique el argumento **format** y use **null** en lugar de una ruta de acceso de archivo de datos.  La opción format siempre requiere la opción **-f** y, para crear un archivo de formato XML, también debe especificar la opción **-x** .  Además, en este ejemplo, el calificador **c** se usa para especificar los datos de caracteres, **t,** se usa para especificar una coma como [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)y **T** se usa para especificar una conexión de confianza que usa seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

El archivo de formato XML, `D:\BCP\myFirstImport.xml` debe tener el aspecto siguiente:
```xml
\<?xml version="1.0"?>
\<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  \<FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  \<FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  \<FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  \<COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  \<COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  \<COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## Usar un archivo de formato para importar datos de forma masiva<a name="import_data"></a>
Los ejemplos siguientes usan la base de datos, el archivo de datos y los archivos de formato que se han creado anteriormente.

### **Uso de [bcp](../../tools/bcp-utility.md) y un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_nonxml"></a>
En el símbolo del sistema, escriba el siguiente comando:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### **Uso de [bcp](../../tools/bcp-utility.md) y un [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bcp_xml"></a>
En el símbolo del sistema, escriba el siguiente comando:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### **Uso de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_nonxml"></a>
Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Uso de [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y un [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bulk_xml"></a>
Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Uso de [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_nonxml"></a>    
Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Uso de [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y [archivo de formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="openrowset_xml"></a>
Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```
  
## <a name="more-examples"></a>Más ejemplos  
 [Crear un archivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Archivos de formato no XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML, archivos de formato &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [Archivos de formato para importar o exportar datos (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
  

