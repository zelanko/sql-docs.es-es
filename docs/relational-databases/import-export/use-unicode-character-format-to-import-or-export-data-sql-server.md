---
title: Uso del formato de caracteres Unicode para importar o exportar datos
description: El formato de datos de caracteres Unicode permite exportar datos desde una instancia de SQL Server mediante una página de códigos diferente de la que usa el cliente.
ms.date: 09/30/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 5e01a35302991de18eb28b8cf458fe1990544eec
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980368"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Uso del formato de caracteres Unicode para importar o exportar datos (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
El formato de caracteres Unicode se recomienda para las transferencias masivas de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un archivo de datos que contenga caracteres DBCS o extendidos. El formato de datos de caracteres Unicode permite exportar datos desde un servidor mediante una página de códigos utilizada por el cliente que está realizando la operación. En esos casos, el uso del formato de caracteres Unicode tiene las siguientes ventajas:  
  
* Si los datos de origen y destino son de tipo Unicode, el uso del formato de caracteres Unicode mantiene todos los datos de los caracteres.  
  
* Si los datos de origen y de destino no son de tipo Unicode, el uso del formato de caracteres Unicode minimiza la pérdida de caracteres extendidos en los datos de origen que no pueden representarse en el destino.

|En este tema:|
|---|
|[Consideraciones sobre el uso del formato de caracteres Unicode](#considerations)|
|[Consideraciones especiales sobre el uso del formato de caracteres Unicode, bcp y un archivo de formato](#special_considerations)|
|[Opciones de comando para el formato de caracteres Unicode](#command_options)|
|[Condiciones de prueba de ejemplo](#etc)<br />&emsp;&#9679;&emsp;[Tabla de ejemplo](#sample_table)<br />&emsp;&#9679;&emsp;[Archivo de formato no XML de ejemplo](#nonxml_format_file)|
|[Ejemplos](#examples)<br />&emsp;&#9679;&emsp;[Usar bcp y el formato de caracteres Unicode para exportar datos](#bcp_widechar_export)<br />&emsp;&#9679;&emsp;[Usar bcp y el formato de caracteres Unicode para importar datos sin un archivo de formato](#bcp_widechar_import)<br />&emsp;&#9679;&emsp;[Usar bcp y el formato de caracteres Unicode para importar datos con un archivo de formato no XML](#bcp_widechar_import_fmt)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y el formato de caracteres Unicode sin un archivo de formato](#bulk_widechar)<br />&emsp;&#9679;&emsp;[Usar BULK INSERT y el formato de caracteres Unicode con un archivo de formato no XML](#bulk_widechar_fmt)<br />&emsp;&#9679;&emsp;[Usar OPENROWSET y el formato de caracteres Unicode con un archivo de formato no XML](#openrowset_widechar_fmt)|
|[Tareas relacionadas](#RelatedTasks)<p>                                                                                                                                                                                                                  </p>|
 
## <a name="considerations-for-using-unicode-character-format"></a>Consideraciones sobre el uso del formato de caracteres Unicode<a name="considerations"></a>
A la hora de usar el formato de caracteres Unicode, tenga en cuenta que:  

* De forma predeterminada, la [utilidad bcp](../../tools/bcp-utility.md) separa los campos de datos de caracteres con el carácter de tabulación y finaliza los registros con el carácter de nueva línea.  Para obtener más información sobre cómo especificar otros terminadores, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).

* Los datos [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md) almacenados en un archivo de datos con formato de caracteres Unicode funcionan de la misma forma que en un archivo de datos en formato de caracteres, con la excepción de que los datos se almacenan como [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) en lugar de almacenarse como [char](../../t-sql/data-types/char-and-varchar-transact-sql.md) . Para obtener más información sobre el formato de caracteres, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  

## <a name="special-considerations-for-using-unicode-character-format-bcp-and-a-format-file"></a>Consideraciones especiales sobre el uso del formato de caracteres Unicode, bcp y un archivo de formato<a name="special_considerations"></a>
Los archivos de datos con formato de caracteres Unicode utilizan las convenciones de los archivos Unicode.  Los primeros dos bytes del archivo son los números hexadecimales 0xFFFE.  Estos bytes funcionan como marcas de orden de bytes (BOM), ya que especifican si el byte de orden alto se almacena el primero o el último en el archivo.  La [utilidad bcp](../../tools/bcp-utility.md) podría malinterpretar la marca de orden de bytes y provocar que parte del proceso de importación dé error. Es posible que reciba un mensaje de error similar al siguiente:
```
Starting copy...
SQLState = 22005, NativeError = 0
Error = [Microsoft][ODBC Driver 13 for SQL Server]Invalid character value for cast specification
```

La marca de orden de bytes podría malinterpretarse en las siguientes condiciones:
* Se usa la [utilidad bcp](../../tools/bcp-utility.md) y el modificador **-w** para indicar el carácter Unicode.

* Se usa un archivo de formato.

* El primer campo del archivo de datos es un campo sin caracteres.

Averigüe si alguna de las siguientes soluciones alternativas está disponible para su situación *concreta* :
* No use ningún archivo de formato.  A continuación se muestra un ejemplo de esta solución alternativa. Consulte [Usar bcp y el formato de caracteres Unicode para importar datos sin un archivo de formato](#bcp_widechar_import).

* Use el modificador **-c** en vez de **-w**.

* Vuelva a exportar los datos con un formato nativo.

* Use [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) u [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  A continuación se muestran ejemplos de estas soluciones alternativas. Consulte [Usar BULK INSERT y el formato de caracteres Unicode con un archivo de formato no XML](#bulk_widechar_fmt) y [Usar OPENROWSET y el formato de caracteres Unicode con un archivo de formato no XML](#openrowset_widechar_fmt).
 
* Inserte manualmente el primer registro en la tabla de destino y, después, use el modificador **-F 2** para que la importación se inicie en el segundo registro.

* Inserte manualmente el primer registro ficticio en el archivo de datos y, después, use el modificador **-F 2** para que la importación se inicie en el segundo registro.  A continuación se muestra un ejemplo de esta solución alternativa. Consulte [Usar bcp y el formato de caracteres Unicode para importar datos con un archivo de formato no XML](#bcp_widechar_import_fmt).

* Use una tabla de almacenamiento provisional en la que la primera columna sea un tipo de datos de caracteres; o

* vuelva a exportar los datos y cambie el orden del campo de datos para que el primer campo de datos sea de caracteres.  Luego, use un archivo de formato para volver a asignar el campo de datos en el orden real de la tabla.  Para ver un ejemplo, consulte [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md).
  
## <a name="command-options-for-unicode-character-format"></a>Opciones de comando para el formato de caracteres Unicode<a name="command_options"></a>  
Puede importar datos del formato de caracteres Unicode en una tabla mediante [bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) o [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md).  Para un comando [bcp](../../tools/bcp-utility.md) o una instrucción [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md), puede especificar el formato de datos en la instrucción.  Para una instrucción [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md), debe especificar el formato de datos en un archivo de formato.  
  
El formato de caracteres Unicode se puede usar con las siguientes opciones de comando:  
  
|Get-Help|Opción|Descripción|  
|-------------|------------|-----------------|  
|BCP|**-w**|Usa el formato de caracteres Unicode.|  
|BULK INSERT|DATAFILETYPE **='widechar'**|Utiliza el formato de caracteres Unicode al importar datos masivamente.|  
|OPENROWSET|N/D|Debe usar un archivo de formato|
  
> [!NOTE]
>  Otra posibilidad es especificar el formato por campo en un archivo de formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).
  
## <a name="example-test-conditions"></a>Condiciones de prueba de ejemplo<a name="etc"></a>  
Los ejemplos de este tema se basan en la tabla y en el archivo de formato definidos a continuación.

### <a name="sample-table"></a>**Tabla de ejemplo**<a name="sample_table"></a>
El siguiente script crea una base de datos de prueba, una tabla denominada `myWidechar` , y la rellena con algunos valores iniciales.  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.myWidechar ( 
    PersonID smallint NOT NULL,
    FirstName nvarchar(25) NOT NULL,
    LastName nvarchar(30) NOT NULL,
    BirthDate date,
    AnnualSalary money
);

-- Populate table
INSERT TestDatabase.dbo.myWidechar
VALUES 
(1, N'ϴAnthony', N'Grosse', '02-23-1980', 65000.00),
(2, N'❤Alica', N'Fatnowna', '11-14-1963', 45000.00),
(3, N'☎Stella', N'Rossenhain', '03-02-1992', 120000.00);

-- Review Data
SELECT * FROM TestDatabase.dbo.myWidechar;
```

### <a name="sample-non-xml-format-file"></a>**Archivo de formato no XML de ejemplo**<a name="nonxml_format_file"></a>
SQL Server admite dos tipos de archivos de formato: XML y no XML.  El formato no XML es el formato original compatible con versiones anteriores de SQL Server.  Revise [Archivos de formato no XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) para obtener información detallada.  El siguiente comando hará uso de la [utilidad BCP](../../tools/bcp-utility.md) para generar un archivo de formato no XML, `myWidechar.fmt`, basado en el esquema de `myWidechar`.  Si quiere usar un comando [BCP](../../tools/bcp-utility.md) para crear un archivo de formato, especifique el argumento **format** y use **null** en lugar de una ruta de acceso de archivo de datos.  La opción format también requiere la opción **-f** .  Además, en este ejemplo, el calificador **c** se usa para especificar los datos de caracteres, mientras que **T** se usa para especificar una conexión de confianza que usa la seguridad integrada.  En un símbolo del sistema, escriba los comandos siguientes:

```
bcp TestDatabase.dbo.myWidechar format nul -f D:\BCP\myWidechar.fmt -T -w

REM Review file
Notepad D:\BCP\myWidechar.fmt
```

> [!IMPORTANT]
> Asegúrese de que el archivo de formato no XML termina con un retorno de carro o avance de línea.  De lo contrario, es probable que reciba el mensaje de error siguiente:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`


## <a name="examples"></a>Ejemplos<a name="examples"></a>
En los siguientes ejemplos se usan la base de datos y los archivos de formato creados anteriormente.

### <a name="using-bcp-and-unicode-character-format-to-export-data"></a>**Usar bcp y el formato de caracteres para exportar datos**<a name="bcp_widechar_export"></a>
Modificador **-w** y comando **OUT** .  Nota: el archivo de datos creado en este ejemplo se usará en todos los ejemplos siguientes.  En un símbolo del sistema, escriba los comandos siguientes:
```
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w

REM Review results
NOTEPAD D:\BCP\myWidechar.bcp
```

### <a name="using-bcp-and-unicode-character-format-to-import-data-without-a-format-file"></a>**Usar bcp y el formato de caracteres Unicode para importar datos sin un archivo de formato**<a name="bcp_widechar_import"></a>
Modificador **-w** y comando **IN** .  En un símbolo del sistema, escriba los comandos siguientes:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Import data
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -T -w

REM Review results is SSMS
```

### <a name="using-bcp-and-unicode-character-format-to-import-data-with-a-non-xml-format-file"></a>**Usar bcp y el formato de caracteres Unicode para importar datos con un archivo de formato no XML**<a name="bcp_widechar_import_fmt"></a>
Modificadores **-w** y **-f** switches y **IN** commy.  Se deberá aplicar una solución alternativa, puesto que este ejemplo implica bcp, un archivo de formato, un carácter Unicode y el primer campo de datos del archivo de datos es un campo sin caracteres.  Consulte la sección [Consideraciones especiales sobre el uso del formato de caracteres Unicode, bcp y un archivo de formato](#special_considerations), que aparece más arriba.  El archivo de datos `myWidechar.bcp` se alterará mediante la adición de un registro adicional como registro "ficticio", que se omitirá con el modificador `-F 2`.

En un símbolo del sistema, escriba los siguientes comandos y siga los pasos de modificación:
```
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.myWidechar;"

REM Open data file
Notepad D:\BCP\myWidechar.bcp
REM Copy first record and then paste as new first record.  This additional record is the "dummy" record.
REM Close file.

REM Import data instructing bcp to skip dummy record with the -F 2 switch.
bcp TestDatabase.dbo.myWidechar IN D:\BCP\myWidechar.bcp -f D:\BCP\myWidechar.fmt -T -F 2

REM Review results is SSMS

REM Return data file to original state for usage in other examples
bcp TestDatabase.dbo.myWidechar OUT D:\BCP\myWidechar.bcp -T -w
```
  
### <a name="using-bulk-insert-and-unicode-character-format-without-a-format-file"></a>**Usar BULK INSERT y el formato de caracteres Unicode sin un archivo de formato**<a name="bulk_widechar"></a>
Argumento**DATAFILETYPE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
    FROM 'D:\BCP\myWidechar.bcp'
    WITH (
        DATAFILETYPE = 'widechar'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### <a name="using-bulk-insert-and-unicode-character-format-with-a-non-xml-format-file"></a>**Usar BULK INSERT y el formato de caracteres Unicode con un archivo de formato no XML**<a name="bulk_widechar_fmt"></a>
Argumento**FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar; -- for testing
BULK INSERT TestDatabase.dbo.myWidechar
   FROM 'D:\BCP\myWidechar.bcp'
   WITH (
        FORMATFILE = 'D:\BCP\myWidechar.fmt'
        );

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
  
### <a name="using-openrowset-and-unicode-character-format-with-a-non-xml-format-file"></a>**Usar OPENROWSET y el formato de caracteres Unicode con un archivo de formato no XML**<a name="openrowset_widechar_fmt"></a>
Argumento**FORMATFILE** .  Ejecutar el siguiente Transact-SQL en Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
TRUNCATE TABLE TestDatabase.dbo.myWidechar;  -- for testing
INSERT INTO TestDatabase.dbo.myWidechar
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myWidechar.bcp', 
        FORMATFILE = 'D:\BCP\myWidechar.fmt'  
        ) AS t1;

-- review results
SELECT * FROM TestDatabase.dbo.myWidechar;
```
 
  
## <a name="related-tasks"></a>Tareas relacionadas<a name="RelatedTasks"></a>
Para usar formatos de datos para la importación o exportación masivas  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
