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
ms.openlocfilehash: a936eb39583afff34dd317b85bc4198022b15e7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920756"
---
# <a name="affectenum"></a>AffectEnum
Especifica qué registros se ven afectados por una operación.  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Si no hay ningún [filtro](../../../ado/reference/ado-api/filter-property.md) aplicado al conjunto de **registros**, afecta a todos los registros.<br /><br /> Si la propiedad **Filter** está establecida en un criterio de cadena (por ejemplo, "author = ' Smith '"), la operación afectará a los registros visibles en el capítulo actual.<br /><br /> Si la propiedad **Filter** está establecida en un miembro de [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) o una matriz de marcadores, la operación afectará a todas las filas del conjunto de **registros**. **Nota: adAffectAll** está oculto en el examinador de objetos Visual Basic.|  
|**adAffectAllChapters**|4|Afecta a todos los registros de todos los capítulos del mismo nivel del **conjunto de registros**, incluidos los que no están visibles a través de cualquier **filtro** aplicado actualmente.|  
|**adAffectCurrent**|1|Afecta solo al registro actual.|  
|**adAffectGroup**|2|Afecta únicamente a los registros que cumplen la configuración de propiedad de [filtro](../../../ado/reference/ado-api/filter-property.md) actual. Debe establecer la propiedad **Filter** en un valor **FilterGroupEnum** o una matriz de **marcadores** para usar esta opción.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. Reverse. ALL|  
|AdoEnums. afecte a. ALLCHAPTERS|  
|AdoEnums. afectar a. CURRENT|  
|AdoEnums. afectar al grupo|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|  
|[Método Resync](../../../ado/reference/ado-api/resync-method.md)|[Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|
