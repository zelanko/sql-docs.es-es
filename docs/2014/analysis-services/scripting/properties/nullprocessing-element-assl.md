---
title: Elemento NullProcessing (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NullProcessing Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7fa4c851e6818a3c9607fed0fdb8b9c499a63d0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139897"
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
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Conservar*|Conserva el valor nulo. **Nota:** este valor no se admite para las medidas de recuento distintivas.|  
|*Error*|Genera un error de clave nula. El valor de [NullKeyNotAllowed](nullkeynotallowed-element-assl.md) determina cómo reacciona la instancia ante el error. **Nota:** este valor no se admite para las medidas.|  
|*UnknownMember*|Genera un miembro desconocido y genera un error de conversión nula. El valor de [NullKeyConvertedToUnknown](nullkeyconvertedtounknown-element-assl.md) determina cómo reacciona la instancia ante el error. **Nota:** este valor no se admite para las columnas asociadas a medidas.|  
|*ZeroOrBlank*|Convierte el valor nulo en cero (para los elementos de datos numéricos) o una cadena vacía (para los elementos de datos de cadena). **Nota:** este valor proporciona compatibilidad con versiones anteriores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Automático*|Utiliza el procesamiento predeterminado adecuado para el elemento:<br /><br /> -   *ZeroOrBlank* para los elementos de datos OLAP.<br />-   *UnknownMember* para elementos de datos de minería de datos.|  
  
 La enumeración que corresponde a los valores permitidos para `NullProcessing` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.NullProcessing>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
