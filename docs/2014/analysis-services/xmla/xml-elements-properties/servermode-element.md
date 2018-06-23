---
title: Elemento ServerMode | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c2f8cb39-dad7-433b-b7b7-fb1625f76a84
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 8448e5ac3111f4c1683ae3dd62dcaef992f3f0e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103400"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
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
  
## <a name="remarks"></a>Notas  
 El servidor opera en cualquiera de los siguientes modos:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Multidimensionales*|Modo multidimensional y de minería de datos|  
|*Tabular*|Modo tabular|  
|*SharePoint*|Modo de SharePoint|  
  
## <a name="see-also"></a>Vea también  
 [Server](../../scripting/objects/server-element-assl.md)  
  
  