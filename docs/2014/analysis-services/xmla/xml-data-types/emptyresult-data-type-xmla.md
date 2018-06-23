---
title: Tipo de datos EmptyResult (XMLA) | Documentos de Microsoft
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
- EmptyResult Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EmptyResult
- olapxmla_EmptyResult
- urn:schemas-microsoft-com:xml-analysis#EmptyResult
helpviewer_keywords:
- EmptyResult data type
ms.assetid: 63818123-acbb-4220-9d60-1aa20a7326a1
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bba727b2d7d612fa59c99665bd16d936da137fb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202585"
---
# <a name="emptyresult-data-type-xmla"></a>Tipo de datos EmptyResult (XMLA)
  Define un tipo de datos derivado que representa un [raíz](../xml-elements-properties/root-element-xmla.md) elemento que no devuelve datos desde una [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) llamada al método.  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis:empty  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:empty">  
   <!-- All elements are inherited from Resultset -->  
</root>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Conjunto de resultados](resultset-data-type-xmla.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|None|  
|Elementos derivados|[raíz](../xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Hay ciertos comandos de MXL for Analysis (MXLA) de los que no se espera que devuelvan un resultado, o puede que no lo devuelvan a causa de un error. Los comandos XMLA que no devuelven un resultado devuelven el tipo de datos `EmptyResult`, un espacio de nombres en el elemento `root`.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo representa un elemento `root` que se ha devuelto para un resultado vacío.  
  
```  
<return>  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty"/>  
</return>  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  