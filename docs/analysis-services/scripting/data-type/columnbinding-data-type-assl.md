---
title: Tipo de datos ColumnBinding (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ColumnBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ColumnBinding
helpviewer_keywords: ColumnBinding data type
ms.assetid: 3ab1bac1-6716-4b17-a107-d5f9c744c5e6
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 86d1f2ee2a1e389cc6d6d8a55b59815cc7546d06
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="columnbinding-data-type-assl"></a>Tipo de datos ColumnBinding (ASSL)
  Define un tipo de datos derivado que representa el enlace de una columna en una vista del origen de datos para un [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) elemento.  
  
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
|Tipos de datos base|[Enlace](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[ColumnID](../../../analysis-services/scripting/properties/columnid-element-eventcolumn-assl.md), [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|Elementos derivados|Vea [enlace](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para crear nombres de elemento XML válidos, [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] **conjunto de datos** objetos codifican los nombres de tabla cuando se serializan en definición de esquemas XML (XSD); por ejemplo, el nombre "Order Details" se convierte en "Order_x0020_Details". Del mismo modo, el **ColumnID** y **TableID** elementos que contienen el **ColumnBinding** elemento y qué objetos de referencia en la vista del origen de datos (DSV) también deben codificar nombres durante la serialización, para garantizar que los nombres coinciden directamente con el texto en la DSV. La instancia de Analysis Services descodificará estos nombres, al igual que el **conjunto de datos** modelo de objetos.  
  
 A **TableDefinitions** elemento incluido en un elemento mediante la **TableBinding** tipo de datos y que hace referencia a tablas en la DSV también deben codificar los nombres cuando se serializan en XSD. Sin embargo, los nombres de tabla en la **partición** enlaces no deberían estar codificados porque son simplemente nombres de tablas que existen en la base de datos y no tiene que estar en la DSV. No codificar la tabla de nombres en el **partición** enlaces también se logra lo siguiente:  
  
-   Mantiene la biblioteca de definiciones de datos (DDL) para las particiones más sencilla.  
  
-   Proporciona más coherencia porque las particiones pueden tener o un nombre de tabla o una instrucción SELECT, y la instrucción SELECT no debería estar codificada.  
  
 Los nombres de tablas y columnas no incluyen delimitadores (por ejemplo, "[" para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
 Para obtener información adicional sobre la **enlace** tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la **enlace** tipo y la jerarquía de herencia de  **Enlace** tipos, consulte [enlazar el tipo de datos &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40; SSAS Multidimensional &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El modelo correspondiente en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.ColumnBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
