---
title: Elemento ServerMode | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8145c7090e1c172fe210202e55078cb4bd404fcb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="servermode-element"></a>Elemento ServerMode
  El **ServerMode** server elemento especifica el modo en que funciona el servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Server>  
...  
   <ddl300:ServerMode>...</ddl300:ServerMode>  
...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|(ninguno)|  
|Cardinalidad|0-1: elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El servidor opera en cualquiera de los siguientes modos:  
  
|Value|Description|  
|-----------|-----------------|  
|*Multidimensionales*|Modo multidimensional y de minería de datos|  
|*Tabular*|Modo tabular|  
|*SharePoint*|Modo de SharePoint|  
  
## <a name="see-also"></a>Vea también  
 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)  
  
  

