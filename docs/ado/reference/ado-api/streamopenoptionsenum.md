---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 091c640ab09cf70cff5e6f7ce3d7bf1dc9dd34ab
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710715"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica opciones para abrir un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Los valores se pueden combinar con una operación de OR.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Se abre el **Stream** objeto en modo asincrónico.|  
|**adOpenStreamFromRecord**|4|Identifica el contenido de la *origen* parámetro sea ya estaba abierto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. El comportamiento predeterminado consiste en tratar *origen* como una dirección URL que apunte directamente a un nodo en una estructura de árbol. Se abre la secuencia predeterminada asociada con ese nodo.|  
|**adOpenStreamUnspecified**|-1|Predeterminado: Especifica la apertura del **Stream** objeto con las opciones predeterminadas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
