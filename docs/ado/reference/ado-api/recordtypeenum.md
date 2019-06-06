---
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eb33d68fcaf32fa92ae9a65e2ca216a86792a1be
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711772"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica el tipo de [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica un *simple* registro (que no contiene nodos secundarios).|  
|**adCollectionRecord**|1|Indica un *colección* registro (que contiene nodos secundarios).|  
|**adRecordUnknown**|-1|Indica que el tipo de este **registro** es desconocido.|  
|**adStructDoc**|2|Indica un especial de *colección* registro que representa COM de documentos estructurados.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Estas constantes no tienen equivalentes de ADO y WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
