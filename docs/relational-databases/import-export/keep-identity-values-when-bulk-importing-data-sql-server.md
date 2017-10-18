---
title: Mantenimiento de valores de identidad al importar datos de forma masiva (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2a20a9d0b7b8cc5aa32863bc687f7095ce33623a
ms.contentlocale: es-es
ms.lasthandoff: 10/13/2017

---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>Mantener valores de identidad al importar datos de forma masiva (SQL Server)
Archivos de datos que contienen valores de identidad que pueden importarse de forma masiva en una instancia de Microsoft SQL Server.  De manera predeterminada, los valores de la columna de identidad del archivo de datos que se importa se omiten y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna automáticamente valores únicos.  Los valores únicos se basan en los valores de inicialización y de incremento especificados durante la creación de la tabla.

Si el archivo de datos no contiene valores para la columna de identificadores de la tabla, use el archivo de formato para especificar que se debe omitir esta columna al importar los datos.  Vea [Usar un archivo de formato para omitir una columna de tabla (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md) para obtener información adicional.

|Esquema|
|---|
|[Mantener valores de identidad](#keep_identity)<br />[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de datos de ejemplo](#sample_data_file)<br />&emsp;&#9679;&emsp;[Archivo de formato no XML de ejemplo](#nonxml_format_file)<br />[Ejemplos](#examples)<br />&emsp;&#9679;&emsp;[Usar BCP y mantener valores de identidad sin un archivo de formato](#bcp_identity)<br />&emsp;&#9679;&emsp;[Usar BCP y mantener valores de identidad con un archivo de formato no XML](#bcp_identity_fmt)<br />&emsp;&#9679;&emsp;[Usar BCP y valores de identidad generados sin un archivo de formato](#bcp_default)<br />&emsp;&#9679;&emsp;[Usar BCP y valores de identidad generados con un archivo de formato no XML](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y mantener valores de identidad sin un archivo de formato](#bulk_identity)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y mantener valores de identidad con un archivo de formato no XML](#bulk_identity_fmt)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y valores de identidad generados sin un archivo de formato](#bulk_default)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y valores de identidad generados con un archivo de formato no XML](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[Usar OPENROWSET y mantener valores de identidad con un archivo de formato no XML](#openrowset_identity_fmt)<br />&emsp;&#9679;&emsp;[Usar OPENROWSET y valores de identidad generados con un archivo de formato no XML](#openrowset_default_fmt)<br /><p>                                                                                                                                                                                                                  </p>|

## Mantener valores de identidad <a name="keep_identity"></a>  
Para impedir que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigne valores de identidad al importar de forma masiva filas de datos en una tabla, utilice el calificador de comando adecuado para mantener la identidad.  Al especificar un calificador para mantener la identidad, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza los valores de identidad del archivo de datos.  Estos calificadores son:

|Command|Calificador para mantener la identidad|Tipo de calificador|  
|-------------|------------------------------|--------------------|  
|bcp|-E|Switch|  
|BULK INSERT|KEEPIDENTITY|Argumento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|Sugerencia de tabla|  
   
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md), [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) y [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  

> [!NOTE]
>  Para crear un número que se incremente automáticamente y que se pueda usar en varias tablas, o que se pueda llamar desde las aplicaciones sin hacer referencia a ninguna tabla, vea [Números de secuencia](../../relational-databases/sequence-numbers/sequence-numbers.md).
 
## Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de este tema se basan en la tabla, en el archivo de datos y en el archivo de formato definidos a continuación.

### **Tabla de ejemplo**<a name="sample_table"></a>
El script siguiente crea una base de datos de prueba y una tabla llamada `myIdentity`.  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myIdentity ( 
   PersonID smallint IDENTITY(1,1) NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date
   );
```
 
### **Archivo de datos de ejemplo**<a name="sample_data_file"></a>
Mediante el Bloc de notas, cree un archivo vacío `D:\BCP\myIdentity.bcp` e inserte los datos siguientes.  
```
3,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
1,Stella,Rosenhain,1992-03-02
4,Miller,Dylan,1954-01-05
```
  
Como alternativa, puede ejecutar el siguiente script de PowerShell para crear y rellenar el archivo de datos:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'myIdentity.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '3,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '1,Stella,Rosenhain,1992-03-02';
Add-Content -Path $bcpFile -Value '4,Miller,Dylan,1954-01-05';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

### **Archivo de formato no XML de ejemplo**<a name="nonxml_format_file"></a>
SQL Server admite dos tipos de archivos de formato: XML y no XML.  El formato no XML es el formato original compatible con versiones anteriores de SQL Server.  Revise [Archivos de formato no XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obtener información detallada.  El siguiente comando hará uso de la [utilidad BCP](../../tools/bcp-utility.md) para generar un archivo de formato no XML, `myIdentity.fmt`, basado en el esquema de `myIdentity`.  Si quiere usar un comando [BCP](../../tools/bcp-utility.md) para crear un archivo de formato, especifique el argumento **format** y use **null** en lugar de una ruta de acceso de archivo de datos.  La opción format también requiere la opción **-f** .  Además, en este ejemplo, el calificador **c** se usa para especificar los datos de caracteres, **t,** se usa para especificar una coma como [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)y **T** se usa para especificar una conexión de confianza que usa seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:
  
```
bcp TestDatabase.dbo.myIdentity format nul -c -f D:\BCP\myIdentity.fmt -t, -T

REM Review file
Notepad D:\BCP\myIdentity.fmt
```
 
> [!IMPORTANT]
> Asegúrese de que el archivo de formato no XML termina con un retorno de carro o avance de línea.  De lo contrario, es probable que reciba el mensaje de error siguiente:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Ejemplos<a name="examples"></a>
Los ejemplos siguientes usan la base de datos, el archivo de datos y los archivos de formato que se han creado anteriormente.
  
### **Usar [BCP](../../tools/bcp-utility.md) y mantener valores de identidad sin un archivo de formato**<a name="bcp_identity"></a>
Modificador**-E** .  En el símbolo del sistema, escriba el siguiente comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t, -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```

### **Usar [BCP](../../tools/bcp-utility.md) y mantener valores de identidad con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_identity_fmt"></a>
Modificadores**-E** y **-f** .  En el símbolo del sistema, escriba el siguiente comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T -E

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
 
### **Usar [BCP](../../tools/bcp-utility.md) y valores de identidad generados sin un archivo de formato**<a name="bcp_default"></a>
Usar valores predeterminados.  En el símbolo del sistema, escriba el siguiente comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -T -c -t,

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Usar [BCP](../../tools/bcp-utility.md) y valores de identidad generados con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
Usar valores predeterminados y el modificador **-f** .  En el símbolo del sistema, escriba el siguiente comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myIdentity;"

REM Import data
bcp TestDatabase.dbo.myIdentity IN D:\BCP\myIdentity.bcp -f D:\BCP\myIdentity.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myIdentity;"
```
  
### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y mantener valores de identidad sin un archivo de formato**<a name="bulk_identity"></a>
Argumento**KEEPIDENTITY** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
    FROM 'D:\BCP\myIdentity.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y mantener valores de identidad con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_identity_fmt"></a>
El argumento**KEEPIDENTITY** y **FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity; -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt',
        KEEPIDENTITY
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y valores de identidad generados sin un archivo de formato**<a name="bulk_default"></a>
Usar valores predeterminados.  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y valores de identidad generados con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
Usar valores predeterminados y el argumento **FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
BULK INSERT dbo.myIdentity
   FROM 'D:\BCP\myIdentity.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myIdentity.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
### **Usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y mantener valores de identidad con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_identity_fmt"></a>
Sugerencia de tabla**KEEPIDENTITY** y argumento **FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
WITH (KEEPIDENTITY) 
(PersonID, FirstName, LastName, BirthDate)
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
 
### **Usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y valores de identidad generados con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_default_fmt"></a>
Usar valores predeterminados y el argumento **FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myIdentity;  -- for testing
INSERT INTO dbo.myIdentity
(FirstName, LastName, BirthDate)
    SELECT FirstName, LastName, BirthDate
    FROM OPENROWSET (
        BULK 'D:\BCP\myIdentity.bcp', 
        FORMATFILE = 'D:\BCP\myIdentity.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myIdentity;
```
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparar los datos para exportar o importar en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar un archivo de formato**  
  
-   [Crear un archivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de datos por razones de compatibilidad cuando se usa bcp**  
  
1.  [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
2.  [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
[Archivos de formato para importar o exportar datos (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)  
  

