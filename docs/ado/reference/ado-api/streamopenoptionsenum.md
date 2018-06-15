---
title: StreamOpenOptionsEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5aca6380229e55ed29c99ea51592e1e618ce0058
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282624"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opciones para abrir un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Los valores pueden combinarse con una operación OR.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Se abre la **flujo** objeto en modo asincrónico.|  
|**adOpenStreamFromRecord**|4|Identifica el contenido de la *origen* parámetro que ya estaba abierto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. El comportamiento predeterminado consiste en tratar *origen* como una dirección URL que apunta directamente a un nodo en una estructura de árbol. Se abre la secuencia predeterminada asociada a ese nodo.|  
|**adOpenStreamUnspecified**|-1|Predeterminado: Especifica la apertura del **flujo** objeto con las opciones predeterminadas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
