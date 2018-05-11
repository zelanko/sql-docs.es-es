---
title: Elemento NullProcessing (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5a33081488c3be0f98f498d31710abb3e742504f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Valor predeterminado|*Automática*|  
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
|*Automática*|Utiliza el procesamiento predeterminado adecuado para el elemento:<br /><br /> *ZeroOrBlank* para los elementos de datos OLAP.<br /><br /> *UnknownMember* para los elementos de datos de la minería de datos.|  
  
 La enumeración que corresponde a los valores permitidos para **NullProcessing** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.NullProcessing>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
