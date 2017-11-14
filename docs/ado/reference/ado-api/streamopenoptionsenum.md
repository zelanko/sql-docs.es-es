---
title: StreamOpenOptionsEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 268d495d2163d03244a6bec57762b93a26ab32ea
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opciones para abrir un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Los valores pueden combinarse con una operación OR.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Se abre la **flujo** objeto en modo asincrónico.|  
|**OpenOptions**|4|Identifica el contenido de la *origen* parámetro que ya estaba abierto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. El comportamiento predeterminado consiste en tratar *origen* como una dirección URL que apunta directamente a un nodo en una estructura de árbol. Se abre la secuencia predeterminada asociada a ese nodo.|  
|**adOpenStreamUnspecified**|-1|Predeterminado: Especifica la apertura del **flujo** objeto con las opciones predeterminadas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)

