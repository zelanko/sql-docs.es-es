---
title: Tipo de datos ResultSet (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Resultset Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Resultset
- urn:schemas-microsoft-com:xml-analysis#Resultset
- Resultset
helpviewer_keywords:
- Resultset data type
ms.assetid: 45e7d7d6-1f89-4dc8-b39d-9270ea2db541
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30d8923c5e3e84c3e2f835caf160902c96c9bf4d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="resultset-data-type-xmla"></a>Tipo de datos Resultset (XMLA)
  Define un tipo de datos primitivo abstracto que representa los datos devueltos desde un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
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
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md), [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md), [conjunto de filas](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Excepción](../../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md), [mensajes](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)|  
|Elementos derivados|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El tipo de datos **Resultset** es un conjunto de resultados XML autodescriptivo que puede incluir tanto esquemas como datos, dependiendo del tipo de información que se vaya a devolver.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  

