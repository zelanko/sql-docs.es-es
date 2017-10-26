---
title: "Mantenimiento de valores NULL o uso de valores predeterminados durante la importación en bloque (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 09/20/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 12b379c1d02dc07a5581a5a3f3585f05f763dad7
ms.openlocfilehash: 74e0dabe8b6691e467e82d7267c40ef578d84490
ms.contentlocale: es-es
ms.lasthandoff: 10/04/2017

---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>Mantener valores NULL o usar valores predeterminados durante la importación masiva (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

De manera predeterminada, cuando se importan datos en una tabla, el comando [BCP](../../tools/bcp-utility.md) y la instrucción [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) aplican los valores predeterminados definidos para las columnas de la tabla.  Por ejemplo, si un archivo de datos contiene un campo NULL, en su lugar, se cargará el valor predeterminado para la columna.  El comando [BCP](../../tools/bcp-utility.md) y la instrucción [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) permiten especificar que se mantengan los valores NULL.

Por el contrario, una instrucción INSERT normal mantiene el valor NULL en lugar de insertar un valor predeterminado. La instrucción INSERT ... La instrucción SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) proporciona el mismo comportamiento básico que la instrucción INSERT regular, pero además admite una [sugerencia de tabla](../../t-sql/queries/hints-transact-sql-table.md) para insertar los valores predeterminados.

|Esquema|
|---|
|[Mantener valores NULL](#keep_nulls)<br />[Usar valores predeterminados con INSERT... SELECT * FROM OPENROWSET(BULK...)](#keep_default)<br />[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de datos de ejemplo](#sample_data_file)<br />&emsp;&#9679;&emsp;[Archivo de formato no XML de ejemplo](#nonxml_format_file)<br />[Mantener valores NULL o usar valores predeterminados durante la importación masiva](#import_data)<br />&emsp;&#9679;&emsp;[Uso de BCP y mantenimiento de valores NULL sin un archivo de formato](#bcp_null)<br />&emsp;&#9679;&emsp;[Uso de BCP y mantenimiento de valores NULL con un archivo de formato no XML](#bcp_null_fmt)<br />&emsp;&#9679;&emsp;[Uso de BCP y uso de valores predeterminados sin un archivo de formato](#bcp_default)<br />&emsp;&#9679;&emsp;[Uso de BCP y uso de valores predeterminados con un archivo de formato no XML](#bcp_default_fmt)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y mantenimiento de valores NULL sin un archivo de formato](#bulk_null)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y mantenimiento de valores NULL con un archivo de formato no XML](#bulk_null_fmt)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y uso de valores predeterminados sin un archivo de formato](#bulk_default)<br />&emsp;&#9679;&emsp;[Uso de BULK INSERT y uso de valores predeterminados con un archivo de formato no XML](#bulk_default_fmt)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y mantenimiento de valores NULL con un archivo de formato no XML](#openrowset__null_fmt)<br />&emsp;&#9679;&emsp;[Uso de OPENROWSET(BULK...) y uso de valores predeterminados con un archivo de formato no XML](#openrowset__default_fmt)

## Mantener valores NULL<a name="keep_nulls"></a>  
Los siguientes calificadores especifican que un campo vacío del archivo de datos mantiene su valor NULL durante la operación de importación masiva, en lugar de heredar un valor predeterminado (si existe) para las columnas de la tabla.  De manera predeterminada, para [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md), cualquier columna no especificada en la operación de carga masiva se establece como NULL.
  
|Command|Qualifier|Tipo de calificador|  
|-------------|---------------|--------------------|  
|BCP|-k|Switch|  
|BULK INSERT|KEEPNULLS**\***|Argumento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|N/D|N/D|  
  
**\*** Para [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), si no hay valores predeterminados disponibles, se debe definir la columna de la tabla para permitir valores NULL. 
  
> [!NOTE]
> Estos calificadores deshabilitan la comprobación de definiciones DEFAULT en una tabla mediante los comandos de importación masiva.  Sin embargo, para cualquier instrucción INSERT simultánea, se esperan definiciones DEFAULT.
 
## Usar valores predeterminados con INSERT... SELECT * FROM [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)<a name="keep_default"></a>  
Puede especificar que para un campo vacío del archivo de datos, la columna de tabla correspondiente use su valor predeterminado (si existe).  Para usar valores predeterminados, use la sugerencia de tabla [KEEPDEFAULTS](../../t-sql/queries/hints-transact-sql-table.md).
 
> [!NOTE]
>  Para más información, vea [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md), [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md), [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) y [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).

## Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de este tema se basan en la tabla, en el archivo de datos y en el archivo de formato definidos a continuación.

### **Tabla de ejemplo**<a name="sample_table"></a>
El script siguiente crea una base de datos de prueba y una tabla llamada `myNulls`.  Tenga en cuenta que la cuarta columna de la tabla, `Kids`, tiene un valor predeterminado.  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myNulls ( 
   PersonID smallint not null,
   FirstName varchar(25),
   LastName varchar(30),
   Kids varchar(13) DEFAULT 'Default Value',
   BirthDate date
   );
```

### **Archivo de datos de ejemplo**<a name="sample_data_file"></a>
Mediante el Bloc de notas, cree un archivo vacío `D:\BCP\myNulls.bcp` e inserte los datos siguientes.  Tenga en cuenta que no hay ningún valor en el registro tercero, cuarta columna.

```
1,Anthony,Grosse,Yes,1980-02-23
2,Alica,Fatnowna,No,1963-11-14
3,Stella,Rosenhain,,1992-03-02
```

Como alternativa, puede ejecutar el siguiente script de PowerShell para crear y rellenar el archivo de datos:

```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = $dir + 'MyNulls.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,Yes,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,No,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```
  
### **Archivo de formato no XML de ejemplo**<a name="nonxml_format_file"></a>
SQL Server admite dos tipos de archivos de formato: XML y no XML.  El formato no XML es el formato original compatible con versiones anteriores de SQL Server.  Revise [Archivos de formato no XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obtener información detallada.  El siguiente comando hará uso de la [utilidad BCP](../../tools/bcp-utility.md) para generar un archivo de formato no XML, `myNulls.fmt`, basado en el esquema de `myNulls`.  Si quiere usar un comando [BCP](../../tools/bcp-utility.md) para crear un archivo de formato, especifique el argumento **format** y use **null** en lugar de una ruta de acceso de archivo de datos.  La opción format también requiere la opción **-f** .  Además, en este ejemplo, el calificador **c** se usa para especificar los datos de caracteres, **t,** se usa para especificar una coma como [terminador de campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)y **T** se usa para especificar una conexión de confianza que usa seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:

```cmd
bcp TestDatabase.dbo.myNulls format nul -c -f D:\BCP\myNulls.fmt -t, -T

REM Review file
Notepad D:\BCP\myNulls.fmt
```

> [!IMPORTANT]
> Asegúrese de que el archivo de formato no XML termina con un retorno de carro o avance de línea.  De lo contrario, es probable que reciba el mensaje de error siguiente:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

 Para obtener más información sobre cómo crear archivos de formato, vea [Crear un archivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
## Mantener valores NULL o usar valores predeterminados durante la importación masiva<a name="import_data"></a>
Los ejemplos siguientes usan la base de datos, el archivo de datos y los archivos de formato que se han creado anteriormente.

### **Usar [BCP](../../tools/bcp-utility.md) y mantener valores NULL sin un archivo de formato**<a name="bcp_null"></a>

Modificador**-k** .  En el símbolo del sistema, escriba el siguiente comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **Usar [BCP](../../tools/bcp-utility.md) y mantener valores NULL con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_null_fmt"></a>
Modificadores**-k** y **-f** . En el símbolo del sistema, escriba el siguiente comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T -k

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **Usar [BCP](../../tools/bcp-utility.md) y usar valores predeterminados sin un archivo de formato**<a name="bcp_default"></a>
En el símbolo del sistema, escriba el siguiente comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -c -t, -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```
  
### **Usar [BCP](../../tools/bcp-utility.md) y usar valores predeterminados con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_default_fmt"></a>
Modificador**-f** .  En el símbolo del sistema, escriba el siguiente comando:

```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myNulls;"

REM Import data
bcp TestDatabase.dbo.myNulls IN D:\BCP\myNulls.bcp -f D:\BCP\myNulls.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myNulls;"
```

### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y mantener valores NULL sin un archivo de formato**<a name="bulk_null"></a>
Argumento**KEEPNULLS** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO
TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
    FROM 'D:\BCP\myNulls.bcp'
    WITH (
        DATAFILETYPE = 'char',  
        FIELDTERMINATOR = ',',  
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y mantener valores NULL con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_null_fmt"></a>
El argumento**KEEPNULLS** y **FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls; -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt',
        KEEPNULLS
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y usar valores predeterminados sin un archivo de formato**<a name="bulk_default"></a>
Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ','
      );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Usar [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y usar valores predeterminados con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_default_fmt"></a>
Argumento**FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
BULK INSERT dbo.myNulls
   FROM 'D:\BCP\myNulls.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myNulls.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y mantener valores NULL con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__null_fmt"></a>
Argumento**FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

### **Usar [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) y usar valores predeterminados con un [archivo de formato no XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset__default_fmt"></a>
Sugerencia de tabla**KEEPDEFAULTS** y argumento **FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):

```sql
USE TestDatabase;
GO

TRUNCATE TABLE dbo.myNulls;  -- for testing
INSERT INTO dbo.myNulls
WITH (KEEPDEFAULTS) 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myNulls.bcp', 
        FORMATFILE = 'D:\BCP\myNulls.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myNulls;
```

  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
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
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  

