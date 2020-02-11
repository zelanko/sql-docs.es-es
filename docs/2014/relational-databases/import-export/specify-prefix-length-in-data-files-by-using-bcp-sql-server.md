---
title: Especificar la longitud de prefijo en los archivos de datos mediante bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], prefix length
- prefix length [SQL Server]
- lengths [SQL Server], prefix characters
- data formats [SQL Server], prefix length
ms.assetid: ce32dd1a-26f1-4f61-b9fa-3f1feea9992e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5d91c82d892888d2e6edde5615ba05a2a9ebf3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011754"
---
# <a name="specify-prefix-length-in-data-files-by-using-bcp-sql-server"></a>Especificar la longitud de prefijo en los archivos de datos mediante bcp (SQL Server)
  Para proporcionar el almacenamiento en archivo más compacto para exportar de forma masiva datos en formato nativo a un archivo de datos, el comando **bcp** precede cada campo con uno o varios caracteres que indican la longitud del campo. Estos caracteres se denominan *caracteres de prefijo de longitud*.  
  
## <a name="the-bcp-prompt-for-prefix-length"></a>Petición bcp de longitud de prefijo  
 Si un comando **bcp** interactivo contiene la opción **in** o **out** sin el modificador de archivo de formato ( **-f**) o un modificador de formato de datos ( **-n**, **-c**, **-w**o **-N**), el comando solicita la longitud de prefijo de cada campo, de la manera siguiente:  
  
 `Enter prefix length of field <field_name> [<default>]:`  
  
 Si especifica 0, **bcp** solicita la longitud del campo (en el caso de un tipo de datos de caracteres) o un terminador de campo (en el caso de un tipo de datos no de caracteres nativo).  
  
> [!NOTE]  
>  Después de que se especifiquen de forma interactiva todos los campos de un comando **bcp**, el comando solicita que guarde sus respuestas para cada campo en un archivo que no tenga el formato XML. Para obtener más información sobre los archivos de formato no XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="overview-of-prefix-length"></a>Información general sobre la longitud de prefijo  
 Para almacenar la longitud de prefijo de un campo, necesita una cantidad de bytes suficiente para representar la longitud máxima del campo. El número de bytes necesario también depende del tipo de almacenamiento de archivo, la nulabilidad de una columna y de si los datos se están almacenando en el archivo de datos en el formato nativo correspondiente o en el formato de caracteres. Por ejemplo, un tipo de datos `text` o `image` necesita cuatro caracteres de prefijo para almacenar la longitud del campo, pero el tipo de datos `varchar` necesita dos caracteres. En el archivo de datos, estos caracteres de prefijo de longitud se almacenan en el formato de datos binario interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Cuando utilice el formato nativo, use prefijos de longitud en lugar de terminadores de campo. El formato de datos nativo puede entrar en conflicto con los terminadores porque en el formato de datos binario interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se almacena un archivo de datos en formato nativo.  
  
##  <a name="PrefixLengthsExport"></a> Longitudes de prefijo para la exportación masiva  
  
> [!NOTE]  
>  El valor predeterminado que se proporciona en la solicitud de longitud de prefijo cuando exporta un campo indica la longitud de prefijo más eficaz para el campo.  
  
 Los valores NULL se representan como un campo vacío. Para indicar que el campo está vacío (representa NULL), el prefijo de campo contiene el valor -1, lo que indica que requiere al menos 1 byte. Recuerde que si la columna de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite valores NULL, la columna requiere una longitud de prefijo de 1 ó más, en función del tipo de almacenamiento de archivo.  
  
 Cuando exporte datos de manera masiva y los almacene en tipos de datos nativos o en formato de caracteres, utilice las longitudes de prefijo de la tabla siguiente:  
  
|SQL Server<br /><br /> tipo de datos|Formato nativo<br /><br /> NOT NULL|Formato nativo<br /><br /> NULL|Formato de caracteres<br /><br /> NOT NULL|Formato de caracteres<br /><br /> NULL|  
|------------------------------|--------------------------------|----------------------------|-----------------------------------|-------------------------------|  
|`char`|2|2|2|2|  
|`varchar`|2|2|2|2|  
|`nchar`|2|2|2|2|  
|`nvarchar`|2|2|2|2|  
|`text`<sup>1</sup>|4|4|4|4|  
|`ntext`<sup>1</sup>|4|4|4|4|  
|`binary`|2|2|2|2|  
|`varbinary`|2|2|2|2|  
|`image`<sup>1</sup>|4|4|4|4|  
|`datetime`|0|1|0|1|  
|`smalldatetime`|0|1|0|1|  
|`decimal`|1|1|1|1|  
|`numeric`|1|1|1|1|  
|`float`|0|1|0|1|  
|`real`|0|1|0|1|  
|`int`|0|1|0|1|  
|`bigint`|0|1|0|1|  
|`smallint`|0|1|0|1|  
|`tinyint`|0|1|0|1|  
|`money`|0|1|0|1|  
|`smallmoney`|0|1|0|1|  
|`bit`|0|1|0|1|  
|`uniqueidentifier`|1|1|0|1|  
|`timestamp`|1|1|1|1|  
|`varchar(max)`|8|8|8|8|  
|`varbinary(max)`|8|8|8|8|  
|UDT (un tipo de datos definido por el usuario)|8|8|8|8|  
|XML|8|8|8|8|  
  
 <sup>1</sup> los `ntext`tipos `text`de datos `image` , y se quitarán en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite su uso en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que los usan actualmente. En `nvarchar(max)`su `varchar(max)`lugar, `varbinary(max)` use, y.  
  
##  <a name="PrefixLengthsImport"></a>Longitudes de prefijo para la importación masiva  
 Cuando los datos se importan de manera masiva, la longitud de prefijo es el valor que se especificó cuando se creó originalmente el archivo de datos. Si el archivo de datos no se creó con un comando **bcp** , probablemente no existan los caracteres de prefijo de longitud. En tal caso, especifique 0 como longitud de prefijo.  
  
> [!NOTE]  
>  Para especificar una longitud de prefijo de un archivo de datos que no se haya creado con **bcp**, use las longitudes indicadas en [Longitudes de prefijo para la exportación masiva](#PrefixLengthsExport)anteriormente en este tema.  
  
## <a name="see-also"></a>Consulte también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especifique la longitud de campo mediante el &#40;BCP SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Especifique File Storage tipo mediante BCP &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  
