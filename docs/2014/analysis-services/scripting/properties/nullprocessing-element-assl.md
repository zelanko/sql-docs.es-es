---
title: Elemento NullProcessing (ASSL) | Documentos de Microsoft
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
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 54b75b2e1a7bddd6f7b5df1aeda0311c1b60ff99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104334"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Automático*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Elemento de datos](../data-type/dataitem-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
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
  
  