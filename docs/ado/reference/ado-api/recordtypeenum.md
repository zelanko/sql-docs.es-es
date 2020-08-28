---
description: RecordTypeEnum
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ded4106b770ff62edd4b79401885ee5ce3101798
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989666"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica el tipo de objeto de [registro](./record-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica un registro *simple* (no contiene nodos secundarios).|  
|**adCollectionRecord**|1|Indica un registro de *colección* (contiene nodos secundarios).|  
|**adRecordUnknown**|-1|Indica que se desconoce el tipo de este **registro** .|  
|**adStructDoc**|2|Indica un tipo especial de registro de *colección* que representa documentos estructurados com.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad RecordType (ADO)](./recordtype-property-ado.md)