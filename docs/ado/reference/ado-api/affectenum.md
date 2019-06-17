---
title: AffectEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d6ff6704ca12fbb20c93133d7e73f29a5f72c9e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696575"
---
# <a name="affectenum"></a>AffectEnum
Especifica qué registros se ven afectados por una operación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Si no hay un [filtro](../../../ado/reference/ado-api/filter-property.md) aplicado a la **Recordset**, afecta a todos los registros.<br /><br /> Si el **filtro** propiedad está establecida en un criterio de cadena (como "autor ="Smith""), la operación afecta a los registros visibles en el capítulo actual.<br /><br /> Si el **filtro** propiedad está establecida en un miembro de la [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) o una matriz de marcadores y, a continuación, la operación afectará a todas las filas de la **Recordset**. **Nota: adAffectAll** está oculto en el Examinador de objetos de Visual Basic.|  
|**adAffectAllChapters**|4|Afecta a todos los registros en todos los capítulos del mismo nivel de la **Recordset**, los que no es visible a través de cualquiera incluidos **filtro** que se aplica actualmente.|  
|**adAffectCurrent**|1|Afecta a solo el registro actual.|  
|**adAffectGroup**|2|Afecta a solo los registros que cumplen actual [filtro](../../../ado/reference/ado-api/filter-property.md) configuración de la propiedad. Debe establecer el **filtro** propiedad a un **FilterGroupEnum** valor o una matriz de **marcadores** para usar esta opción.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Affect.ALL|  
|AdoEnums.Affect.ALLCHAPTERS|  
|AdoEnums.Affect.CURRENT|  
|AdoEnums.Affect.GROUP|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|  
|[Método Resync](../../../ado/reference/ado-api/resync-method.md)|[Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|
