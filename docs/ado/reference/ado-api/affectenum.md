---
title: AffectEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3192f84f0dd09bdb6d2479e090d1adb5c0b25fe
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="affectenum"></a>AffectEnum
Especifica que los registros se ven afectados por una operación.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Si no hay un [filtro](../../../ado/reference/ado-api/filter-property.md) aplicado a la **Recordset**, afecta a todos los registros.<br /><br /> Si el **filtro** propiedad se establece en un criterio de cadena (como "autor = 'Smith'"), la operación afecta a registros visibles en el capítulo actual.<br /><br /> Si el **filtro** propiedad se establece en un miembro de la [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) o una matriz de marcadores y, a continuación, la operación afectará a todas las filas de la **conjunto de registros**. **Nota:****adAffectAll** está oculto en el Examinador de objetos de Visual Basic.|  
|**adAffectAllChapters**|4|Afecta a todos los registros de todos los capítulos relacionados de la **Recordset**, los que no es visible a través de cualquiera incluidos **filtro** que se aplica actualmente.|  
|**adAffectCurrent**|1|Afecta a solo el registro actual.|  
|**adAffectGroup**|2|Afecta a solo los registros que satisfagan actual [filtro](../../../ado/reference/ado-api/filter-property.md) configuración de la propiedad. Debe establecer el **filtro** propiedad a una **FilterGroupEnum** valor o una matriz de **marcadores** para usar esta opción.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
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
