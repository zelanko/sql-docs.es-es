---
title: Usar las propiedades de celda (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- intrinsic cell properties [MDX]
- cells [MDX]
- cell properties [MDX]
- CELL PROPERTIES keyword
ms.assetid: a593c74d-8c5e-485e-bd92-08f9d22451d4
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 496fbb18fa454b17b78dc54d598a96a88e5dcb8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104136"
---
# <a name="using-cell-properties-mdx"></a>Usar las propiedades de celda (MDX)
  Las propiedades de celda de las expresiones multidimensionales (MDX) contienen información sobre el contenido y el formato de las celdas de un origen de datos multidimensional, como un cubo.  
  
 MDX admite la palabra clave CELL PROPERTIES en una instrucción MDX SELECT para recuperar propiedades de celda intrínsecas. Las propiedades de celda intrínsecas se suelen utilizar para facilitar la presentación visual de los datos de las celdas.  
  
## <a name="cell-properties-keyword-syntax"></a>Sintaxis de la palabra clave CELL PROPERTIES  
 Use la siguiente sintaxis para la `CELL PROPERTIES` palabra clave de MDX `SELECT` instrucción:  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 La siguiente sintaxis muestra el formato del valor `<cell_props>` y cómo éste utiliza la palabra clave `CELL PROPERTIES` junto con una o más propiedades de celda intrínsecas:  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>Propiedades de celda intrínsecas compatibles  
 En la siguiente tabla figuran las propiedades de celda intrínsecas compatibles que se utilizan en el valor `<property>` .  
  
|Property|Descripción|  
|--------------|-----------------|  
|`ACTION_TYPE`|Máscara de bits que indica los tipos de acciones de la celda. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> Nota: Las acciones de obtención de detalles no se incluyen para las consultas que contienen un conjunto en la cláusula WHERE.|  
|**BACK_COLOR**|Color de fondo para mostrar las propiedades `VALUE` o `FORMATTED_VALUE`. Para obtener más información, vea [Contenido de FORE_COLOR y BACK_COLOR &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|`CELL_ORDINAL`|Número ordinal de la celda en el conjunto de datos.|  
|**FONT_FLAGS**|Máscara de bits que detalla los efectos de la fuente. Por ejemplo, el valor 5 representa la combinación de negrita (`MDFF_BOLD`) y subrayado (`MDFF_UNDERLINE`) efectos de fuente. El valor es el resultado de una operación de bits OR de una o varias de las siguientes constantes:<br /><br /> `MDFF_BOLD` = 1<br /><br /> `MDFF_ITALIC` = 2<br /><br /> `MDFF_UNDERLINE` = 4<br /><br /> `MDFF_STRIKEOUT` = 8|  
|**FONT_NAME**|La fuente que se utilizará para mostrar el `VALUE` o `FORMATTED_VALUE` propiedad.|  
|**FONT_SIZE**|Tamaño de fuente utilizado para mostrar la propiedad `VALUE` o `FORMATTED_VALUE`.|  
|**FORE_COLOR**|Color de primer plano para mostrar las propiedades `VALUE` o `FORMATTED_VALUE`. Para obtener más información, vea [Contenido de FORE_COLOR y BACK_COLOR &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|`FORMAT`|Igual que `FORMAT_STRING`.|  
|`FORMAT_STRING`|La cadena de formato utilizada para crear la `FORMATTED_VALUE` valor de propiedad. Para obtener más información, vea [FORMAT_STRING, contenido &#40;MDX&#41;](mdx-cell-properties-format-string-contents.md).|  
|`FORMATTED_VALUE`|La cadena de caracteres que representa una visualización con formato de la `VALUE` propiedad.|  
|`LANGUAGE`|Configuración regional a la que se aplicará `FORMAT_STRING`. `LANGUAGE` suele utilizarse para la conversión de moneda.|  
|`UPDATEABLE`|Valor que indica si la celda puede actualizarse. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> `MD_MASK_ENABLED` (0 x 00000000) la celda puede actualizarse.<br /><br /> `MD_MASK_NOT_ENABLED` (0 x 10000000) no se puede actualizar la celda.<br /><br /> `CELL_UPDATE_ENABLED` (0 x 00000001) celda puede actualizarse en el conjunto de celdas.<br /><br /> `CELL_UPDATE_ENABLED_WITH_UPDATE` (0 x 00000002) la celda puede actualizarse con una instrucción update. La actualización puede no realizarse correctamente si se actualiza una celda hoja no habilitada para escritura.<br /><br /> `CELL_UPDATE_NOT_ENABLED_FORMULA` (0 x 10000001) la celda no se puede actualizar porque la celda tiene un miembro calculado entre sus coordenadas; la celda se ha recuperado con un conjunto de where cláusula. Las celdas pueden actualizarse incluso si tienen una fórmula que incida en el valor de una celda, o si hay una celda calculada activa (en algún punto de la ruta de agregación). Con este escenario, es posible que el valor final de la celda no sea el valor actualizado, puesto que el cálculo afecta al resultado.<br /><br /> `CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE` (0 x 10000002) la celda no se puede actualizar porque no se pueden actualizar las medidas de no suma (count, min, max, distinct count, semiaditivas).<br /><br /> `CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE` (0 x 10000003) la celda no se puede actualizar porque la celda no existe tal y como se encuentra en la intersección de una medida y un miembro de dimensión no relacionados con el grupo de medida de la medida.<br /><br /> `CELL_UPDATE_NOT_ENABLED_SECURE` (0 x 10000005) la celda no se puede actualizar porque está protegida.<br /><br /> `CELL_UPDATE_NOT_ENABLED_CALCLEVEL` (0 x 10000006) reservado para uso futuro.<br /><br /> `CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE` (0 x 10000007) la celda no se puede actualizar por motivos internos.<br /><br /> `CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE` (0 x 10000009) la celda no se puede actualizar porque no se admite la actualización en el modelo de minería de datos, indirecta o dimensiones de minería de datos.|  
|`VALUE`|Valor sin formato de la celda.|  
  
 Solo el `CELL_ORDINAL`, `FORMATTED_VALUE`, y `VALUE` son necesarias las propiedades de celda. Todas las propiedades de celda, intrínsecas o específicas del proveedor, se definen en el conjunto de datos del esquema `PROPERTIES`, incluidos los tipos de datos y la compatibilidad con el proveedor. Para obtener más información sobre la `PROPERTIES` de filas de esquema, consulte [filas MDSCHEMA_PROPERTIES](../../schema-rowsets/ole-db-olap/mdschema-properties-rowset.md).  
  
 De forma predeterminada, si la `CELL PROPERTIES` no se utiliza la palabra clave, las propiedades de celda devueltas son `VALUE`, `FORMATTED_VALUE`, y `CELL_ORDINAL` (en ese orden). Si el `CELL PROPERTIES` se utiliza la palabra clave, se devuelven únicamente las propiedades de celda especificadas explícitamente con la palabra clave.  
  
 En el ejemplo siguiente se muestra el uso de la `CELL PROPERTIES` palabra clave en una consulta MDX:  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 Propiedades de celda no se devuelven en las consultas MDX que devuelven conjuntos de filas planas; en este caso, cada celda se representa como si sólo el `FORMATTED_VALUE` devolvió la propiedad de celda.  
  
## <a name="setting-cell-properties"></a>Establecer las propiedades de celda  
 Las propiedades de celda se pueden establecer en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en diversos sitios. Por ejemplo, la propiedad Cadena de formato se puede establecer para medidas normales en la pestaña Estructura de cubo del Editor de cubos en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]; la misma propiedad puede establecerse para medidas calculadas definidas en el cubo en la pestaña Cálculos del Editor de cubos; las medidas calculadas definidas en la cláusula WITH de una consulta también definen su cadena de formato aquí. La consulta siguiente muestra cómo las propiedades de celda se pueden establecer sobre una medida calculada:  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  