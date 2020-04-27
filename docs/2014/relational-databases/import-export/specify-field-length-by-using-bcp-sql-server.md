---
title: Especificar la longitud de campo mediante bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- default field lengths
- field length [SQL Server]
- data formats [SQL Server], field length
- bcp utility [SQL Server], field length
ms.assetid: 240f33ca-ef4a-413a-a4de-831885cb505b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abb451611f7e102e9167561ef2c3a4b64e00fb12
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011841"
---
# <a name="specify-field-length-by-using-bcp-sql-server"></a>Especificar la longitud de campo mediante bcp (SQL Server)
  La longitud de campo indica el número máximo de caracteres necesarios para representar los datos en formato de carácter. La longitud de campo se conoce si los datos están almacenados en formato nativo; por ejemplo, el tipo de datos `int` ocupa 4 bytes. Si ha indicado 0 para la longitud del prefijo, el comando **BCP** le solicitará la longitud del campo, las longitudes de campo predeterminadas y el impacto de la longitud de campo en el `char` almacenamiento de datos en los archivos de datos que contienen datos.  
  
## <a name="the-bcp-prompt-for-field-length"></a>Solicitud bcp para la longitud de campo  
 Si un comando **bcp** interactivo contiene la opción **in** o **out** sin el modificador de archivo de formato ( **-f**) o un modificador de formato de datos ( **-n**, **-c**, **-w** o **-N**), el comando solicita la longitud de campo de cada campo, de la manera siguiente:  
  
 `Enter length of field <field_name> [<default>]:`  
  
 Para obtener un ejemplo que muestra esta solicitud en contexto, vea [Especificar formatos de datos por razones de compatibilidad mediante bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  Después de que se especifiquen de forma interactiva todos los campos de un comando **bcp**, el comando solicita que guarde sus respuestas para cada campo en un archivo que no tenga el formato XML. Para obtener más información sobre los archivos con formato distinto de XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
 Que un comando **bcp** solicite la longitud de campo depende de varios factores, entre ellos los siguientes:  
  
-   Cuando se copian tipos de datos que no son de longitud fija y se especifica una longitud de prefijo 0, **bcp** solicita una longitud de campo.  
  
-   Cuando se convierten datos que no son de caracteres al formato de datos de caracteres, **bcp** recomienda una longitud de campo predeterminada lo suficientemente grande como para almacenar los datos.  
  
-   Si se almacenan tipos de archivos que no son de caracteres, el comando **bcp** no solicita una longitud de campo. Los datos se almacenan en la representación de datos nativa de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (formato nativo).  
  
## <a name="using-default-field-lengths"></a>Usar longitudes de campo predeterminadas  
 Por lo general, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda aceptar los valores predeterminados que sugiere **bcp**para la longitud de campo. Cuando se crea un archivo de datos en modo de carácter, si especifica la longitud de campo predeterminada, los datos no se truncan ni se producirán errores de desbordamiento numérico.  
  
 Si especifica una longitud de campo incorrecta, pueden producirse problemas. Por ejemplo, si copia datos numéricos y especifica una longitud de campo demasiado corta para los datos, la utilidad **bcp** imprime un mensaje de desbordamiento y no copia los datos. Además, si exporta `datetime` datos y especifica una longitud de campo inferior a 26 bytes para la cadena de caracteres, la utilidad **BCP** trunca los datos sin un mensaje de error.  
  
> [!IMPORTANT]  
>  Cuando se utiliza la opción de tamaño predeterminado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera leer una cadena entera. En algunos casos, el uso de la longitud de campo predeterminada puede provocar un error del tipo "fin de archivo inesperado". Normalmente, este error se produce con `money` los `datetime` tipos de datos y cuando solo parte del campo esperado tiene lugar en el archivo de datos; por ejemplo, cuando un `datetime` valor de *mm*/*DD*/*AA* se especifica sin el componente de hora y es, por lo tanto, menor que la longitud esperada de `datetime` 24 caracteres `char` de un valor en formato. Para evitar este tipo de error, puede utilizar terminadores de campo o campos de datos de longitud fija o cambiar la longitud de campo predeterminada especificando otro valor.  
  
### <a name="default-field-lengths-for-character-file-storage"></a>Longitudes de campo predeterminadas para el almacenamiento de archivos de caracteres  
 En la siguiente tabla se enumeran las longitudes de campo predeterminadas de los datos que se almacenan como tipo de almacenamiento de archivo de caracteres. Los datos que aceptan valores NULL tienen la misma longitud que los datos que no aceptan valores NULL.  
  
|Tipo de datos|Longitud predeterminada (caracteres)|  
|---------------|-----------------------------------|  
|`char`|Longitud definida para la columna|  
|`varchar`|Longitud definida para la columna|  
|`nchar`|Dos veces la longitud definida para la columna|  
|`nvarchar`|Dos veces la longitud definida para la columna|  
|`Text`|0|  
|`ntext`|0|  
|`bit`|1|  
|`binary`|Dos veces la longitud definida para la columna + 1|  
|`varbinary`|Dos veces la longitud definida para la columna + 1|  
|`image`|0|  
|`datetime`|24|  
|`smalldatetime`|24|  
|`float`|30|  
|`real`|30|  
|`int`|12|  
|`bigint`|19|  
|`smallint`|7|  
|`tinyint`|5|  
|`money`|30|  
|`smallmoney`|30|  
|`decimal`|41*|  
|`numeric`|41*|  
|`uniqueidentifier`|37|  
|`timestamp`|17|  
|`varchar(max)`|0|  
|`varbinary(max)`|0|  
|`nvarchar(max)`|0|  
|UDT|Longitud de la columna del término definido por el usuario (UDT)|  
|XML|0|  
  
 \*Para obtener más información sobre `decimal` los `numeric` tipos de datos y, vea [decimal y numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql).  
  
> [!NOTE]  
>  Una columna de tipo `tinyint` puede contener valores entre 0 y 255; el número máximo de caracteres necesarios para representar cualquier número de este intervalo es tres (que representa valores entre 100 y 255).  
  
### <a name="default-field-lengths-for-native-file-storage"></a>Longitudes de campo predeterminadas para el almacenamiento de archivos nativos  
 En la siguiente tabla se enumeran las longitudes de campo predeterminadas de los datos que se almacenan como tipo de almacenamiento de archivos nativos. Los datos que aceptan valores NULL tienen la misma longitud que los datos que no aceptan valores NULL, y los datos de caracteres siempre se almacenan en formato de caracteres.  
  
|Tipo de datos|Longitud predeterminada (caracteres)|  
|---------------|-----------------------------------|  
|`bit`|1|  
|`binary`|Longitud definida para la columna|  
|`varbinary`|Longitud definida para la columna|  
|`image`|0|  
|`datetime`|8|  
|`smalldatetime`|4|  
|`float`|8|  
|`real`|4|  
|`int`|4|  
|`bigint`|8|  
|`smallint`|2|  
|`tinyint`|1|  
|`money`|8|  
|`smallmoney`|4|  
|`decimal`<sup>1</sup>|<sup>*</sup>|  
|`numeric`<sup>1</sup>|<sup>*</sup>|  
|`uniqueidentifier`|16|  
|`timestamp`|8|  
  
 <sup>1</sup> para obtener más información sobre `decimal` los `numeric` tipos de datos y, vea [decimal y Numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql).  
  
 En todos los casos anteriores, si desea crear un archivo de datos para recargarlo posteriormente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y mantener el espacio de almacenamiento mínimo, use un prefijo de longitud con el tipo de almacenamiento en archivo y la longitud de campo predeterminados.  
  
## <a name="see-also"></a>Consulte también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)   
 [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
  
