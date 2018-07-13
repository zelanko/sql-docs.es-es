---
title: Tipo de datos ColumnBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ColumnBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnBinding
helpviewer_keywords:
- ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 227801af8b66d66ebeba50d2713267720adffa9a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200115"
---
# <a name="columnbinding-data-type-assl"></a>Tipo de datos ColumnBinding (ASSL)
  Define un tipo de datos derivado que representa el enlace de una columna en una vista del origen de datos a un [DataItem](dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ColumnBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
      <ColumnID>...</ColumnID>  
</ColumnBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Enlace](binding-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[ColumnID](../properties/columnid-element-eventcolumn-assl.md), [TableID](../properties/id-element-assl.md)|  
|Elementos derivados|Consulte [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 Para crear nombres de elemento XML válidos, [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] `DataSet` objetos codifican los nombres de tabla cuando se serializan en XML Schema Definition (XSD); por ejemplo, el nombre "Order Details" se convierte en "Order_x0020_Details". Asimismo, los elementos `ColumnID` y  `TableID` que están incluidos en el elemento `ColumnBinding` y que hacen referencia a objetos de la vista del origen de datos (DSV) también deben codificar los nombres durante la serialización para garantizar que los nombres coinciden directamente con el texto de la DSV. La instancia de Analysis Services descodificará estos nombres, al igual que el modelo de objetos `DataSet`.  
  
 Un elemento `TableDefinitions` que está incluido en un elemento, que utiliza el tipo de datos `TableBinding` y que hace referencia a tablas de la DSV también debe codificar los nombres cuando se serializan en XSD. Sin embargo, los nombres de tabla de los enlaces `Partition` no deberían estar codificados porque son simplemente nombres de tablas que existen en la base de datos y no tienen que estar en la DSV. Al no codificar los nombres de tabla en los enlaces `Partition`, también se logra lo siguiente:  
  
-   Mantiene la biblioteca de definiciones de datos (DDL) para las particiones más sencilla.  
  
-   Proporciona más coherencia porque las particiones pueden tener o un nombre de tabla o una instrucción SELECT, y la instrucción SELECT no debería estar codificada.  
  
 Los nombres de tablas y columnas no incluyen delimitadores (por ejemplo, "[" para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, vea [tipo de enlace de datos &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El modelo correspondiente en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.ColumnBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
