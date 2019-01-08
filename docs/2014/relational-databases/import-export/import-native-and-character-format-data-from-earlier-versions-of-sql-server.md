---
title: Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a87863d3046de695e489e83ec46eb073a7f4761c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531597"
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]puede usar **bcp** para importar datos con formato nativo y de caracteres de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] con el modificador **-V** . El modificador **-V** hace que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] use los tipos de datos de la versión anterior especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y el formato del archivo de datos es el mismo que el de esa versión anterior.  
  
 Para especificar una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para un archivo de datos, use el modificador **-V** con uno de los siguientes calificadores:  
  
|Versión de SQL Server|Qualifier|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>Interpretación de los tipos de datos  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores tienen compatibilidad para algunos nuevos tipos. Si desea importar un tipo de datos nuevo en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe almacenarlo en un formato que pueda ser leído por la versión anterior de los clientes **bcp** . En la tabla siguiente se resume cómo se convierten los tipos de datos nuevos a efectos de compatibilidad con las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nuevos tipos de datos de SQL Server 2005|Tipos de datos compatibles de la versión 6*x*|Tipos de datos compatibles de la versión 70|Tipos de datos compatibles de la versión 80|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|`bigint`|`decimal`|`decimal`|*|  
|`sql_variant`|`text`|`nvarchar(4000)`|*|  
|`varchar(max)`|`text`|`text`|`text`|  
|`nvarchar(max)`|`ntext`|`ntext`|`ntext`|  
|`varbinary(max)`|`image`|`image`|`image`|  
|XML|`ntext`|`ntext`|`ntext`|  
|UDT<sup>1</sup>|`image`|`image`|`image`|  
  
 \* Este tipo es compatible de forma nativa.  
  
 <sup>1</sup> UDT indica un tipo definido por el usuario.  
  
## <a name="exporting-using--v-80"></a>Exportación mediante -V 80  
 Al exportar masivamente datos mediante el uso de la **-V80** cambiar, `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, XML, y se almacenan datos UDT en modo nativo con un prefijo de 4 bytes, como `text`, `image`y `ntext`datos, en lugar de con un prefijo de 8 bytes, que es el valor predeterminado para [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores.  
  
## <a name="copying-date-values"></a>Copiar valores de fecha  
 **bcp** utiliza la API de copia masiva de ODBC. Por tanto, para importar valores de fecha en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **bcp** usa el formato de fecha ODBC (*yyyy-mm-dd hh:mm:ss*[*.f...*]).  
  
 El **bcp** comando exporta los archivos de datos de formato de caracteres utilizando el formato predeterminado ODBC para `datetime` y `smalldatetime` valores. Por ejemplo, una columna `datetime` que contiene la fecha `12 Aug 1998` se copia de forma masiva en un archivo de datos como la cadena de caracteres `1998-08-12 00:00:00.000`.  
  
> [!IMPORTANT]  
>  Cuando importe datos en un `smalldatetime` campo mediante **bcp**, asegúrese de que el valor de los segundos sea 00.000; de lo contrario, se producirá un error de la operación. El tipo de datos `smalldatetime` contiene únicamente valores hasta el minuto más cercano. BULK INSERT e INSERT ... SELECT * FROM OPENROWSET(BULK...) no darán error en esta instancia, pero truncarán el valor de los segundos.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST y CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
