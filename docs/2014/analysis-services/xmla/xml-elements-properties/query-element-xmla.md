---
title: Consulta de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Query Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Query
- microsoft.xml.analysis.query
- http://schemas.microsoft.com/analysisservices/2003/engine#Query
helpviewer_keywords:
- Query element
ms.assetid: 5a4544e4-012f-4a47-942c-23596400ea16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68da02ef99a5668c7ee0a3a57a06aca90ae68a25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224405"
---
# <a name="query-element-xmla"></a>Elemento Query (XMLA)
  Contiene una consulta dentro de la [consultas](queries-element-xmla.md) colección usada por el [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md) comando durante la optimización basada en uso.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Queries>  
   ...  
   <Query>...</Query>  
   ...  
</Queries>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Consultas](queries-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El comando `DesignAggregations` admite la optimización basada en el uso incluyendo uno o más elementos `Query` en la colección `Queries` del comando. Cada `Query` elemento representa una consulta de objetivo que utiliza el proceso de diseño para definir agregaciones dirigidas a las consultas utilizadas con frecuencia. Puede especificar sus propias consultas de objetivo, o puede usar la información almacenada por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en el registro de consultas para recuperar información sobre con más frecuencia utiliza las consultas.  
  
 Si está diseñando agregaciones de forma iterativa, solo tiene que pasar las consultas de objetivo en la primera `DesignAggregations` comando porque el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia almacena estas consultas de objetivo y las usa durante la subsiguiente `DesignAggregations` comandos. Después de incluir las consultas del objetivo en el primer comando `DesignAggregations` de un proceso iterativo, cualquier comando `DesignAggregations` posterior que contenga las consultas de objetivo en la propiedad `Queries` generará un error.  
  
 El elemento `Query` contiene un valor delimitado por comas que contiene los siguientes argumentos:  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *Frecuencia*  
 Un factor de ponderación que corresponde al número de veces que se ha ejecutado con anterioridad la consulta. Si el `Query` elemento representa una consulta nueva, el *frecuencia* valor representa el factor de ponderación utilizado por el proceso de diseño para evaluar la consulta. A medida que el valor de frecuencia se vuelve mayor, el valor de ponderación que se asigna a la consulta durante el proceso de diseño va aumentando.  
  
 *Conjunto de datos*  
 Una cadena numérica que especifica qué atributos de una dimensión se van a incluir en la consulta. Esta cadena debe tener el mismo número de caracteres que el número de atributos de la dimensión. El cero (0) indica que el atributo de la posición ordinal especificada no está incluido en la consulta de la dimensión especificada, mientras que el uno (1) indica que el atributo de la posición ordinal especificada está incluido en la consulta de la dimensión especificada.  
  
 Por ejemplo, la cadena "011" haría referencia a una consulta que implicaría una dimensión con tres atributos, de los que el segundo y el tercero estarían incluidos en la consulta.  
  
> [!NOTE]  
>  Algunos atributos no se tienen en cuenta en el conjunto de datos. Para obtener más información sobre los atributos excluidos, vea [Properties (XMLA)](query-element-xmla.md).  
  
 Cada dimensión del grupo de medida que contiene el diseño de agregaciones está representada por un *Dataset* valor en el `Query` elemento. El orden de los valores de *Dataset* debe coincidir con el orden de las dimensiones incluidas en el grupo de medidas.  
  
## <a name="see-also"></a>Vea también  
 [Diseño de agregaciones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/designing-aggregations-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
