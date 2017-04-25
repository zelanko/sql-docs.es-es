---
title: Especificar el tipo de almacenamiento en archivo mediante bcp (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fc454960a271c4fdfeb5e04337b2fb8ab1790127
ms.lasthandoff: 04/11/2017

---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>Especificar el tipo de almacenamiento en archivo mediante bcp (SQL Server)
  El *tipo de almacenamiento en archivo* describe cómo se almacenan los datos en el archivo de datos. La información se puede exportar a un archivo de datos como el tipo de tabla de base de datos correspondiente (formato nativo), como su representación en caracteres (formato de caracteres) o como cualquier tipo de datos que admita la conversión implícita (por ejemplo, si copia un elemento **smallint** como **int**). Los tipos de datos definidos por el usuario se exportan como sus tipos base correspondientes.  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>Comando bcp para el tipo de almacenamiento en archivo  
 Si un comando **bcp** interactivo contiene la opción **in** u **out** sin el modificador de archivo de formato (**-f**) o un modificador de formato de datos (**-n**, **-c**, **-w**o **-N**), el comando solicita el tipo de almacenamiento de archivos de cada campo de datos, de la manera siguiente:  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 Su respuesta a este mensaje depende de la tarea que realice:  
  
-   Para exportar datos de forma masiva desde una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos con el almacenamiento más compacto posible (formato de datos nativo), acepte los tipos de almacenamiento de archivos predeterminados que proporciona **bcp**. Para obtener una lista de los tipos de almacenamiento en archivo nativos, vea "Tipos de almacenamiento en archivo nativos", más adelante en este mismo tema.  
  
-   Para exportar datos de forma masiva desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos en formato de caracteres, especifique **char** como el tipo de almacenamiento en archivo para todas las columnas de la tabla.  
  
-   Para importar datos en bloque a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un archivo de datos, especifique el tipo de almacenamiento en archivo como **char** para los tipos almacenados en formato de caracteres y, para los datos almacenados en formato de tipo de datos nativo, especifique uno de los siguientes tipos de almacenamiento en archivo, según corresponda:  
  
    |tipo de almacenamiento en archivo|Escriba en el símbolo del sistema|  
    |-----------------------|-----------------------------|  
    |**char***|**c**[**har**]|  
    |**varchar**|**c[har]**|  
    |**nchar**|**w**|  
    |**nvarchar**|**w**|  
    |**texto***\*|**T**[**ext**]|  
    |**ntext2**|**W**|  
    |**binario**|**x**|  
    |**varbinary**|**x**|  
    |**imagen***\*|**I**[**mage**]|  
    |**datetime**|**d[ate]**|  
    |**smalldatetime**|**D**|  
    |**time**|**te**|  
    |**date**|**de**|  
    |**datetime2**|**d2**|  
    |**datetimeoffset**|**do**|  
    |**decimal**|**n**|  
    |**numeric**|**n**|  
    |**float**|**f[loat]**|  
    |**real**|**r**|  
    |**Int**|**i[nt]**|  
    |**bigint**|**B[igint]**|  
    |**smallint**|**s[mallint]**|  
    |**tinyint**|**t[inyint]**|  
    |**money**|**m[oney]**|  
    |**smallmoney**|**M**|  
    |**bit**|**b[it]**|  
    |**uniqueidentifier**|**u**|  
    |**sql_variant**|**V[ariant]**|  
    |**timestamp**|**x**|  
    |**UDT** (un tipo de datos definido por el usuario)|**U**|  
    |**XML**|**X**|  
  
     \*La interacción de longitud de campo, longitud de prefijo y terminadores determina la cantidad de espacio de almacenamiento que se asigna en un archivo de datos a datos que no son de caracteres que se exportan como el tipo de almacenamiento de archivos **char** .  
  
     \*\* Los tipos de datos **ntext**, **text**e **image** se quitarán en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En proyectos de desarrollo nuevos evite el uso de estos tipos de datos y planee la modificación de las aplicaciones que los utilicen actualmente. Use **nvarchar(max)**, **varchar(max)**y **varbinary(max)** en su lugar.  
  
## <a name="native-file-storage-types"></a>Tipos de almacenamiento en archivo nativos  
 Cada tipo de almacenamiento en archivo nativo se registra en el archivo de formato como el tipo de datos de archivo host correspondiente.  
  
|tipo de almacenamiento en archivo|Tipo de datos del archivo host|  
|-----------------------|-------------------------|  
|**char***|SQLCHAR|  
|**varchar**|SQLCHAR|  
|**nchar**|SQLNCHAR|  
|**nvarchar**|SQLNCHAR|  
|**texto***\*|SQLCHAR|  
|**ntext***\*|SQLNCHAR|  
|**binario**|SQLBINARY|  
|**varbinary**|SQLBINARY|  
|**imagen***\*|SQLBINARY|  
|**datetime**|SQLDATETIME|  
|**smalldatetime**|SQLDATETIM4|  
|**decimal**|SQLDECIMAL|  
|**numeric**|SQLNUMERIC|  
|**float**|SQLFLT8|  
|**real**|SQLFLT4|  
|**int**|SQLINT|  
|**bigint**|SQLBIGINT|  
|**smallint**|SQLSMALLINT|  
|**tinyint**|SQLTINYINT|  
|**money**|SQLMONEY|  
|**smallmoney**|SQLMONEY4|  
|**bit**|SQLBIT|  
|**uniqueidentifier**|SQLUNIQUEID|  
|**sql_variant**|SQLVARIANT|  
|**timestamp**|SQLBINARY|  
|UDT (un tipo de datos definido por el usuario)|SQLUDT|  
  
 \*Los archivos de datos que se almacenan en formato de caracteres usan **char** como tipo de almacenamiento de archivos. Por consiguiente, para archivos de datos de caracteres, SQLCHAR es el único tipo de datos que aparece en un archivo de formato.  
  
 \*\*No puede importar datos en bloque en columnas **text**, **ntext**e **image** que tengan valores DEFAULT.  
  
## <a name="additional-considerations-for-file-storage-types"></a>Consideraciones adicionales para los tipos de almacenamiento en archivo  
 Cuando exporta datos de forma masiva desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un archivo de datos:  
  
-   Siempre puede especificar **char** como tipo de almacenamiento en archivo.  
  
-   Si indica un tipo de almacenamiento en archivo que representa una conversión implícita no válida, se produce un error en **bcp** ; por ejemplo, aunque puede especificar **int** para datos **smallint** , si especifica **smallint** para datos **int** , se producirán errores de desbordamiento.  
  
-   Si se almacenan tipos de datos que no son de caracteres (por ejemplo, **float**, **money**, **datetime**o **int** ) como los tipos de bases de datos correspondientes, los datos se escribirán con el formato nativo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el archivo de datos.  
  
    > [!NOTE]  
    >  Después de que se especifiquen de forma interactiva todos los campos de un comando **bcp**, el comando solicita que guarde sus respuestas para cada campo en un archivo que no tenga el formato XML. Para obtener más información sobre los archivos con formato distinto de XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Especificar la longitud de campo mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)   
 [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
