---
title: Elemento NullProcessing (ASSL) | Documentos de Microsoft
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NullProcessing Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc5c99e52f8868251d7d5b581bdefcea6e5d3097
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
  Define cómo se procesan los valores nulos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataItem>  
   ...  
   <NullProcessing>...</NullProcessing>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Automático*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Conservar*|Conserva el valor nulo.<br /><br /> Nota: Este valor no se admite para las medidas de recuento distintivas.|  
|*Error*|Genera un error de clave nula. El valor de [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md) determina cómo reacciona la instancia ante el error.<br /><br /> Nota: Este valor no se admite para las medidas.|  
|*UnknownMember*|Genera un miembro desconocido y genera un error de conversión nula. El valor de [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md) determina cómo reacciona la instancia ante el error.<br /><br /> Nota: Este valor no se admite para las columnas asociadas a medidas.|  
|*ZeroOrBlank*|Convierte el valor nulo en cero (para los elementos de datos numéricos) o una cadena vacía (para los elementos de datos de cadena).<br /><br /> Nota: Este valor proporciona compatibilidad con versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Automático*|Utiliza el procesamiento predeterminado adecuado para el elemento:<br /><br /> *ZeroOrBlank* para los elementos de datos OLAP.<br /><br /> *UnknownMember* para los elementos de datos de la minería de datos.|  
  
 La enumeración que corresponde a los valores permitidos para **NullProcessing** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.NullProcessing>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

