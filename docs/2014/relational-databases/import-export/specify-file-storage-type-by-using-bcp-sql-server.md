---
title: Especificar el tipo de almacenamiento en archivo mediante bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a3646aa6ef61c820ca5512203b0ff1e36894cab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011818"
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>Especificar el tipo de almacenamiento en archivo mediante bcp (SQL Server)
  El *tipo de almacenamiento en archivo* describe cómo se almacenan los datos en el archivo de datos. La información se puede exportar a un archivo de datos como el tipo de tabla de base de datos correspondiente (formato nativo), como su representación en caracteres (formato de caracteres) o como cualquier tipo de datos que admita la conversión implícita (por ejemplo, si copia datos `smallint` como datos `int`). Los tipos de datos definidos por el usuario se exportan como sus tipos base correspondientes.  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>Comando bcp para el tipo de almacenamiento de archivos  
 Si un comando **bcp** interactivo contiene la opción **in** u **out** sin el modificador de archivo de formato (**-f**) o un modificador de formato de datos (**-n**, **-c**, **-w**o **-N**), el comando solicita el tipo de almacenamiento de archivos de cada campo de datos, de la manera siguiente:  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 Su respuesta a este mensaje depende de la tarea que realice:  
  
-   Para exportar datos de forma masiva desde una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos con el almacenamiento más compacto posible (formato de datos nativo), acepte los tipos de almacenamiento de archivos predeterminados que proporciona **bcp**. Para obtener una lista de los tipos de almacenamiento en archivo nativos, vea "Tipos de almacenamiento en archivo nativos", más adelante en este mismo tema.  
  
-   Para exportar datos de forma masiva desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos en formato de caracteres, especifique `char` como el tipo de almacenamiento en archivo para todas las columnas de la tabla.  
  
-   Para importar datos de forma masiva a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un archivo de datos, especifique el tipo de almacenamiento en archivo como `char` para los tipos almacenados en formato de caracteres y, para los datos almacenados en formato de tipo de datos nativo, especifique uno de los siguientes tipos de almacenamiento en archivo, según corresponda:  
  
    |tipo de almacenamiento en archivo|Escriba en el símbolo del sistema|  
    |-----------------------|-----------------------------|  
    |`char`<sup>1</sup>|`c`[`har`]|  
    |`varchar`|`c[har]`|  
    |`nchar`|`w`|  
    |`nvarchar`|`w`|  
    |`text`<sup>2</sup>|`T`[`ext`]|  
    |`ntext2`|`W`|  
    |`binary`|`x`|  
    |`varbinary`|`x`|  
    |`image`<sup>2</sup>|`I`[`mage`]|  
    |`datetime`|**d [ar]**|  
    |`smalldatetime`|`D`|  
    |`time`|`te`|  
    |`date`|`de`|  
    |`datetime2`|`d2`|  
    |`datetimeoffset`|`do`|  
    |`decimal`|`n`|  
    |`numeric`|`n`|  
    |`float`|**f [Loat]**|  
    |`real`|`r`|  
    |`Int`|**i [NT]**|  
    |`bigint`|`B[igint]`|  
    |`smallint`|**s [despelusa]**|  
    |`tinyint`|**t [inyint]**|  
    |`money`|**m [Oney]**|  
    |`smallmoney`|`M`|  
    |`bit`|`b[it]`|  
    |`uniqueidentifier`|`u`|  
    |`sql_variant`|`V[ariant]`|  
    |`timestamp`|`x`|  
    |`UDT`(un tipo de datos definido por el usuario)|`U`|  
    |`XML`|`X`|  
  
     <sup>1</sup> la interacción de longitud de campo, longitud de prefijo y terminadores determina la cantidad de espacio de almacenamiento que se asigna en un archivo de datos para datos que no son `char` de caracteres que se exporta como tipo de almacenamiento de archivos.  
  
     <sup>2</sup> los `ntext`tipos `text`de datos `image` , y se quitarán en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En proyectos de desarrollo nuevos evite el uso de estos tipos de datos y planee la modificación de las aplicaciones que los utilicen actualmente. En `nvarchar(max)`su `varchar(max)`lugar, `varbinary(max)` use, y.  
  
## <a name="native-file-storage-types"></a>Tipos de almacenamiento en archivo nativos  
 Cada tipo de almacenamiento en archivo nativo se registra en el archivo de formato como el tipo de datos de archivo host correspondiente.  
  
|tipo de almacenamiento en archivo|Tipo de datos del archivo host|  
|-----------------------|-------------------------|  
|`char`<sup>1</sup>|SQLCHAR|  
|`varchar`|SQLCHAR|  
|`nchar`|SQLNCHAR|  
|`nvarchar`|SQLNCHAR|  
|`text`<sup>2</sup>|SQLCHAR|  
|`ntext`<sup>2</sup>|SQLNCHAR|  
|`binary`|SQLBINARY|  
|`varbinary`|SQLBINARY|  
|`image`<sup>2</sup>|SQLBINARY|  
|`datetime`|SQLDATETIME|  
|`smalldatetime`|SQLDATETIM4|  
|`decimal`|SQLDECIMAL|  
|`numeric`|SQLNUMERIC|  
|`float`|SQLFLT8|  
|`real`|SQLFLT4|  
|`int`|SQLINT|  
|`bigint`|SQLBIGINT|  
|`smallint`|SQLSMALLINT|  
|`tinyint`|SQLTINYINT|  
|`money`|SQLMONEY|  
|`smallmoney`|SQLMONEY4|  
|`bit`|SQLBIT|  
|`uniqueidentifier`|SQLUNIQUEID|  
|`sql_variant`|SQLVARIANT|  
|`timestamp`|SQLBINARY|  
|UDT (un tipo de datos definido por el usuario)|SQLUDT|  
  
 <sup>1</sup> los archivos de datos que se almacenan en `char` formato de caracteres utilizan como tipo de almacenamiento de archivos. Por consiguiente, para archivos de datos de caracteres, SQLCHAR es el único tipo de datos que aparece en un archivo de formato.  
  
 <sup>2</sup> no se pueden importar datos de `text`forma `ntext`masiva en `image` columnas, y que tengan valores predeterminados.  
  
## <a name="additional-considerations-for-file-storage-types"></a>Consideraciones adicionales para los tipos de almacenamiento de archivos  
 Cuando exporta datos de forma masiva desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos:  
  
-   Siempre puede especificar `char` como tipo de almacenamiento en archivo.  
  
-   Si especifica un tipo de almacenamiento en archivo que representa una conversión implícita no válida, se produce un error en **BCP** ; por ejemplo, aunque puede `int` especificar para `smallint` los datos, si especifica `smallint` para `int` los datos, se producirán errores de desbordamiento.  
  
-   Si se almacenan tipos de datos que no son de caracteres (por ejemplo, `float`, `money`, `datetime` o `int` como los tipos de bases de datos correspondientes, los datos se escribirán con el formato nativo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el archivo de datos.  
  
    > [!NOTE]  
    >  Después de que se especifiquen de forma interactiva todos los campos de un comando **bcp**, el comando solicita que guarde sus respuestas para cada campo en un archivo que no tenga el formato XML. Para obtener más información sobre los archivos con formato distinto de XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especifique la longitud de campo mediante el &#40;BCP SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Especifique la longitud del prefijo en los archivos de datos mediante BCP &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
