---
title: Tipo de datos ResultSet (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Resultset Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Resultset
- urn:schemas-microsoft-com:xml-analysis#Resultset
- Resultset
helpviewer_keywords:
- Resultset data type
ms.assetid: 45e7d7d6-1f89-4dc8-b39d-9270ea2db541
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a34b99aa63608faafa42d94aaf8938f86bb3894c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205495"
---
# <a name="resultset-data-type-xmla"></a>Tipo de datos Resultset (XMLA)
  Define un tipo de datos primitivo abstracto que representa los datos devueltos desde un [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) llamada al método.  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis:resultset  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Resultset>  
   <Exception>...</Exception>  
   <Messages>...</Messages>  
</Resultset>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[MDDataSet](mddataset-data-type-xmla.md), [olapxmla_EmptyResult](emptyresult-data-type-xmla.md), [conjunto de filas](rowset-data-type-xmla.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Excepción](../xml-elements-properties/exception-element-xmla.md), [mensajes](../xml-elements-properties/messages-element-xmla.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentarios  
 El tipo de datos `Resultset` es un conjunto de resultados XML autodescriptivo que puede incluir tanto esquemas como datos, dependiendo del tipo de información que se vaya a devolver.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
