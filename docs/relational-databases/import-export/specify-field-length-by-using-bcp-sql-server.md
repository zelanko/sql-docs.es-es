---
title: Especificar la longitud de campo mediante bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- default field lengths
- field length [SQL Server]
- data formats [SQL Server], field length
- bcp utility [SQL Server], field length
ms.assetid: 240f33ca-ef4a-413a-a4de-831885cb505b
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5bda4afe1b3c6b64ea1609412be66de03fa6329e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32940150"
---
# <a name="specify-field-length-by-using-bcp-sql-server"></a>Especificar la longitud de campo mediante bcp (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  La longitud de campo indica el número máximo de caracteres necesarios para representar los datos en formato de carácter. La longitud de campo se conoce si los datos están almacenados en formato nativo; por ejemplo, el tipo de datos **int** ocupa 4 bytes. Si ha indicado 0 para la longitud del prefijo, el comando **bcp** le solicitará la longitud del campo, las longitudes predeterminadas de los campos y los efectos de la longitud del campo en el almacenamiento de datos en los archivos de datos que contienen datos de tipo **char** .  
  
## <a name="the-bcp-prompt-for-field-length"></a>Solicitud bcp para la longitud de campo  
 Si un comando **bcp** interactivo contiene la opción **in** o **out** sin el modificador de archivo de formato (**-f**) o un modificador de formato de datos (**-n**, **-c**, **-w** o **-N**), el comando solicita la longitud de campo de cada campo, de la manera siguiente:  
  
 `Enter length of field <field_name> [<default>]:`  
  
 Para obtener un ejemplo que muestra esta solicitud en contexto, vea [Especificar formatos de datos por razones de compatibilidad mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  Después de que se especifiquen de forma interactiva todos los campos de un comando **bcp**, el comando solicita que guarde sus respuestas para cada campo en un archivo que no tenga el formato XML. Para obtener más información sobre los archivos con formato distinto de XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
 Que un comando **bcp** solicite la longitud de campo depende de varios factores, entre ellos los siguientes:  
  
-   Cuando se copian tipos de datos que no son de longitud fija y se especifica una longitud de prefijo 0, **bcp** solicita una longitud de campo.  
  
-   Cuando se convierten datos que no son de caracteres al formato de datos de caracteres, **bcp** recomienda una longitud de campo predeterminada lo suficientemente grande como para almacenar los datos.  
  
-   Si se almacenan tipos de archivos que no son de caracteres, el comando **bcp** no solicita una longitud de campo. Los datos se almacenan en la representación de datos nativa de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (formato nativo).  
  
## <a name="using-default-field-lengths"></a>Usar longitudes de campo predeterminadas  
 Por lo general, [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda aceptar los valores predeterminados que sugiere **bcp**para la longitud de campo. Cuando se crea un archivo de datos en modo de carácter, si especifica la longitud de campo predeterminada, los datos no se truncan ni se producirán errores de desbordamiento numérico.  
  
 Si especifica una longitud de campo incorrecta, pueden producirse problemas. Por ejemplo, si copia datos numéricos y especifica una longitud de campo demasiado corta para los datos, la utilidad **bcp** imprime un mensaje de desbordamiento y no copia los datos. Asimismo, si exporta datos **datetime** y especifica una longitud de campo inferior a 26 bytes para la cadena de caracteres, la utilidad **bcp** trunca los datos sin mostrar un mensaje de error.  
  
> [!IMPORTANT]  
>  Cuando se utiliza la opción de tamaño predeterminado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera leer una cadena entera. En algunos casos, el uso de la longitud de campo predeterminada puede provocar un error del tipo "fin de archivo inesperado". Normalmente, este error se produce con tipos de datos **money** y **datetime** cuando en el archivo de datos solo tiene lugar parte del campo esperado. Por ejemplo, cuando se especifica un valor **datetime** de *mm*/*dd*/*aa* sin el componente de hora y, por tanto, su longitud es inferior a los 24 caracteres esperados de un valor **datetime** en formato **char** . Para evitar este tipo de error, puede utilizar terminadores de campo o campos de datos de longitud fija o cambiar la longitud de campo predeterminada especificando otro valor.  
  
### <a name="default-field-lengths-for-character-file-storage"></a>Longitudes de campo predeterminadas para el almacenamiento de archivos de caracteres  
 En la siguiente tabla se enumeran las longitudes de campo predeterminadas de los datos que se almacenan como tipo de almacenamiento de archivo de caracteres. Los datos que aceptan valores NULL tienen la misma longitud que los datos que no aceptan valores NULL.  
  
|Tipo de datos|Longitud predeterminada (caracteres)|  
|---------------|-----------------------------------|  
|**char**|Longitud definida para la columna|  
|**varchar**|Longitud definida para la columna|  
|**nchar**|Dos veces la longitud definida para la columna|  
|**nvarchar**|Dos veces la longitud definida para la columna|  
|**Texto**|0|  
|**ntext**|0|  
|**bit**|1|  
|**binario**|Dos veces la longitud definida para la columna + 1|  
|**varbinary**|Dos veces la longitud definida para la columna + 1|  
|**imagen**|0|  
|**datetime**|24|  
|**smalldatetime**|24|  
|**float**|30|  
|**real**|30|  
|**int**|12|  
|**bigint**|19|  
|**smallint**|7|  
|**tinyint**|5|  
|**money**|30|  
|**smallmoney**|30|  
|**decimal**|41*|  
|**numeric**|41*|  
|**uniqueidentifier**|37|  
|**timestamp**|17|  
|**ntext**|0|  
|**varbinary(max)**|0|  
|**nvarchar(max)**|0|  
|UDT|Longitud de la columna del término definido por el usuario (UDT)|  
|XML|0|  
  
 \*Para más información sobre los tipos de datos **decimal** y **numeric**, vea [Datos decimal y numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
> [!NOTE]  
>  Una columna de tipo **tinyint** puede contener valores entre 0 y 255. El número máximo de caracteres necesarios para representar cualquier número de este rango es tres (que representa valores entre 100 y 255).  
  
### <a name="default-field-lengths-for-native-file-storage"></a>Longitudes de campo predeterminadas para el almacenamiento de archivos nativos  
 En la siguiente tabla se enumeran las longitudes de campo predeterminadas de los datos que se almacenan como tipo de almacenamiento de archivos nativos. Los datos que aceptan valores NULL tienen la misma longitud que los datos que no aceptan valores NULL, y los datos de caracteres siempre se almacenan en formato de caracteres.  
  
|Tipo de datos|Longitud predeterminada (caracteres)|  
|---------------|-----------------------------------|  
|**bit**|1|  
|**binario**|Longitud definida para la columna|  
|**varbinary**|Longitud definida para la columna|  
|**imagen**|0|  
|**datetime**|8|  
|**smalldatetime**|4|  
|**float**|8|  
|**real**|4|  
|**int**|4|  
|**bigint**|8|  
|**smallint**|2|  
|**tinyint**|1|  
|**money**|8|  
|**smallmoney**|4|  
|**decimal**|*|  
|**numeric**|*|  
|**uniqueidentifier**|16|  
|**timestamp**|8|  
  
 \*Para más información sobre los tipos de datos **decimal** y **numeric**, vea [Datos decimal y numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 En todos los casos anteriores, si desea crear un archivo de datos para recargarlo posteriormente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y mantener el espacio de almacenamiento mínimo, use un prefijo de longitud con el tipo de almacenamiento en archivo y la longitud de campo predeterminados.  
  
## <a name="see-also"></a>Ver también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)   
 [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)   
 [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
  
