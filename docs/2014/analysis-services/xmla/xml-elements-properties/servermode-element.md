---
title: Elemento ServerMode | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e714c9f5bbc7626030d83faa7d0058c7aa13752
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140185"
---
# <a name="servermode-element"></a>Elemento ServerMode
  El elemento del servidor de `ServerMode` especifica el modo en que el servidor está funcionando.  
  
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
|Elementos primarios|[Server](../../scripting/objects/server-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El servidor opera en cualquiera de los siguientes modos:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Multidimensionales*|Modo multidimensional y de minería de datos|  
|*Tabular*|Modo tabular|  
|*SharePoint*|Modo de SharePoint|  
  
## <a name="see-also"></a>Vea también  
 [Server](../../scripting/objects/server-element-assl.md)  
  
  
