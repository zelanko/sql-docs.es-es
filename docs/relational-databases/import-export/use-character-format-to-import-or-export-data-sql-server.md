---
title: Usar el formato de caracteres para importar o exportar datos (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 09/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: babd3dc4daaa60af026d8694e0cc69292ab44ce0
ms.lasthandoff: 04/11/2017

---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>Usar el formato de caracteres para importar o exportar datos (SQL Server)
Se recomienda utilizar el formato de caracteres al exportar datos de forma masiva a un archivo de texto que se va a utilizar en otro programa o al importar datos de forma masiva desde un archivo de texto generado por otro programa.  

El formato de caracteres utiliza el formato de datos de caracteres para todas las columnas. El almacenamiento de información en el formato de caracteres resulta útil si se utilizan los datos en otro programa, como hojas de cálculo, o bien cuando es necesario copiar los datos a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una base de datos de otro proveedor, como Oracle.  
  
> [!NOTE]
>  Para transferir datos masivamente entre instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el archivo de datos contiene caracteres Unicode pero no contiene caracteres extendidos o DBCS, utilice el formato de caracteres Unicode. Para obtener más información, vea [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).
  
|En este tema:|
|---|
|[Consideraciones acerca del uso del formato de caracteres](#considerations)|
|[Opciones de comando para el formato de caracteres](#command_options)|
|[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de formato no XML de ejemplo](#nonxml_format_file)<br />|
|[Ejemplos](#examples)<br />&emsp;&#9679;&emsp;[Usar bcp y el formato de caracteres para exportar datos](#bcp_char_export)<br />&emsp;&#9679;&emsp;[Usar bcp y el formato de caracteres para importar datos sin un archivo de formato](#bcp_char_import)<br />&emsp;&#9679;&emsp;[Usar bcp y el formato de caracteres para importar datos con un archivo de formato no XML](#bcp_char_import_fmt)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y el formato de caracteres sin un archivo de formato](#bulk_char)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y el formato de caracteres con un archivo de formato no XML](#bulk_char_fmt)<br />&emsp;&#9679;&emsp;[Usar OPENROWSET y el formato de caracteres con un archivo de formato no XML](#openrowset_char_fmt)|
|[Tareas relacionadas](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|


  
## Consideraciones acerca del uso del formato de caracteres<a name="considerations"></a>
Al utilizar el formato de caracteres, tenga en cuenta que:  
  
-   De forma predeterminada, la [utilidad bcp](../../tools/bcp-utility.md) separa los campos de datos de caracteres con el carácter de tabulación y finaliza los registros con el carácter de nueva línea.  Para obtener más información sobre cómo especificar otros terminadores, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
-   De forma predeterminada, antes de la exportación o importación masiva de los datos en modo de caracteres, se realizan las conversiones siguientes:  
  
    |Dirección de la operación masiva|Conversión|  
    |---------------------------------|----------------|  
    |Exportar|Convierte los datos en representaciones de caracteres. Si se solicita de forma explícita, los datos se convierten a la página de códigos solicitada para las columnas de caracteres. Si no se especifica ninguna página de códigos, los datos de caracteres se convierten mediante la página de códigos OEM del equipo cliente.|  
    |Importar|Convierte los datos de caracteres en representaciones nativas, cuando es necesario, y traduce los datos de caracteres de la página de códigos del cliente a la página de códigos de las columnas de destino.|  
  
-   Para evitar la pérdida de caracteres extendidos durante la conversión, utilice el formato de caracteres Unicode o especifique una página de códigos.  
  
-   Todos los datos [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) almacenados en un archivo de formato de caracteres se almacenan sin metadatos. Cada valor de dato se convierte al formato [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) , según las reglas de conversión implícita de datos. Cuando los datos se importan en la columna [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) , se importan como [char](../../t-sql/data-types/char-and-varchar-transact-sql.md). Cuando los datos se importan en una columna con un tipo de datos diferente de [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md), se convierten desde [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) mediante la conversión implícita. Para obtener más información sobre la conversión de datos, vea [Conversiones de tipos de datos &#40;motor de base de datos&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).  
  
-   La [utilidad bcp](../../tools/bcp-utility.md) exporta valores [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) como archivos de datos con formato de caracteres con cuatro cifras tras el separador decimal y sin símbolos de agrupación de cifras, tales como separadores de millares. Por ejemplo, una columna [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) que contenga el valor 1.234.567,123456 se exportará de forma masiva a un archivo de datos como la cadena de caracteres 1234567,1235.  
  
## Opciones de comando para el formato de caracteres<a name="command_options"></a>  
Puede importar datos en formato de caracteres en una tabla usando [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md). Para un comando [bcp](../../tools/bcp-utility.md) o una instrucción [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), puede especificar el formato de datos en la instrucción.  Para una instrucción [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), debe especificar el formato de datos en un archivo de formato.  
  
El formato de caracteres se puede usar con las siguientes opciones de comando:  
  
|Command|Opción|Descripción|  
|-------------|------------|-----------------|  
|bcp|**-c**|Hace que la utilidad bcp use datos de caracteres.*|  
|BULK INSERT|DATAFILETYPE **='char'**|Utiliza el formato de caracteres al importar datos masivamente.|  
|OPENROWSET|N/D|Debe usar un archivo de formato|
  
 \*Para cargar datos de caracteres (**-c**) en un formato compatible con versiones anteriores de clientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use el modificador **-V** . Para obtener más información, vea [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
   
> [!NOTE]
>  Otra posibilidad es especificar el formato por campo en un archivo de formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).

## Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de este tema se basan en la tabla y en el archivo de formato definidos a continuación.

### **Tabla de ejemplo**<a name="sample_table"></a>
El siguiente script crea una base de datos de prueba, una tabla denominada `myChar` , y la rellena con algunos valores iniciales.  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myChar ( 
   PersonID smallint NOT NULL,
   FirstName varchar(25) NOT NULL,
   LastName varchar(30) NOT NULL,
   BirthDate date,
   AnnualSalary money
   );

-- Populate table
INSERT TestDatabase.dbo.myChar
VALUES 
(1, 'Anthony', 'Grosse', '1980-02-23', 65000.00),
(2, 'Alica', 'Fatnowna', '1963-11-14', 45000.00),
(3, 'Stella', 'Rossenhain', '1992-03-02', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Archivo de formato no XML de ejemplo**<a name="nonxml_format_file"></a>
SQL Server admite dos tipos de archivos de formato: XML y no XML.  El formato no XML es el formato original compatible con versiones anteriores de SQL Server.  Revise [Archivos de formato no XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obtener información detallada.  El siguiente comando hará uso de la [utilidad BCP](../../tools/bcp-utility.md) para generar un archivo de formato no XML, `myChar.fmt`, basado en el esquema de `myChar`.  Si quiere usar un comando [BCP](../../tools/bcp-utility.md) para crear un archivo de formato, especifique el argumento **format** y use **null** en lugar de una ruta de acceso de archivo de datos.  La opción format también requiere la opción **-f** .  Además, en este ejemplo, el calificador **c** se usa para especificar los datos de caracteres, mientras que **T** se usa para especificar una conexión de confianza que usa la seguridad integrada.  En el símbolo del sistema, escriba el siguiente comando:

```
bcp TestDatabase.dbo.myChar format nul -f D:\BCP\myChar.fmt -T -c 

REM Review file
Notepad D:\BCP\myChar.fmt
```

> [!IMPORTANT]
> Asegúrese de que el archivo de formato no XML termina con un retorno de carro o avance de línea.  De lo contrario, es probable que reciba el mensaje de error siguiente:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

## Ejemplos<a name="examples"></a>
En los siguientes ejemplos se usan la base de datos y los archivos de formato creados anteriormente.

### **Usar el formato de caracteres para importar o exportar datos**<a name="bcp_char_export"></a>
Modificador**-c** y comando **OUT** .  Nota: el archivo de datos creado en este ejemplo se usará en todos los ejemplos siguientes.  En el símbolo del sistema, escriba el siguiente comando:
```
bcp TestDatabase.dbo.myChar OUT D:\BCP\myChar.bcp -T -c

REM Review results
NOTEPAD D:\BCP\myChar.bcp
```

### **Usar bcp y el formato de caracteres para importar datos sin un archivo de formato**<a name="bcp_char_import"></a>
Modificador**-c** y comando **IN** .  En el símbolo del sistema, escriba el siguiente comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -T -c

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **Usar bcp y el formato de caracteres para importar datos con un archivo de formato no XML**<a name="bcp_char_import_fmt"></a>
Modificadores**-c** y **-f** switches y **IN** commy.  En el símbolo del sistema, escriba el siguiente comando:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myChar;"

REM Import data
bcp TestDatabase.dbo.myChar IN D:\BCP\myChar.bcp -f D:\BCP\myChar.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.myChar;"
```

### **Usar BULK INSERT y el formato de caracteres sin un archivo de formato**<a name="bulk_char"></a>
Argumento**DATAFILETYPE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
    FROM 'D:\BCP\myChar.bcp'
    WITH (
        DATAFILETYPE = 'Char'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Usar BULK INSERT y el formato de caracteres con un archivo de formato no XML**<a name="bulk_char_fmt"></a>
Argumento**FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
TRUNCATE TABLE TestDatabase.dbo.myChar; -- for testing
BULK INSERT TestDatabase.dbo.myChar
   FROM 'D:\BCP\myChar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myChar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```

### **Usar OPENROWSET y el formato de caracteres con un archivo de formato no XML**<a name="openrowset_char_fmt"></a>
Argumento**FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```tsql
TRUNCATE TABLE TestDatabase.dbo.myChar;  -- for testing
INSERT INTO TestDatabase.dbo.myChar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myChar.bcp', 
        FORMATFILE = 'D:\BCP\myChar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myChar;
```
  
## Tareas relacionadas<a name="RelatedTasks"></a>  
Para usar formatos de datos para la importación o exportación masivas 
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  

