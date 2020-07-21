---
title: Recommendation (DTA, elemento) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: stevestein
ms.author: sstein
ms.openlocfilehash: ebb2d9fc4e6c060aaee348297ab1732ffb2eb2a9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040294"
---
# <a name="recommendation-element-dta"></a>Recommendation (DTA, elemento)
  Contiene información sobre los índices hipotéticos que forman parte de una configuración especificada por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento `Table`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Table &#40;DTA, elemento de Schema&#41;](table-element-for-schema-dta.md)|  
|**Elementos secundarios**|[Create &#40;DTA, elemento&#41;](create-element-dta.md)<br /><br /> Elemento `Drop`. Para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Observaciones  
 Este elemento tiene el nombre **RecommendationTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. Se utiliza para especificar índices para una configuración hipotética. No confunda este elemento `Recommendation` con los otros tipos que se pueden utilizar para especificar particiones (`RecommendationPType`) o vistas (`RecommendationViewType`). Para obtener información sobre estos otros `Recommendation` tipos de elementos, vea el [esquema XML de Asistente para la optimización de motor de base de datos](https://go.microsoft.com/fwlink/?linkid=43100).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
