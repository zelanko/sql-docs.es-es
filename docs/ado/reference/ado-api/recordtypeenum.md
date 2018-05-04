---
title: RecordTypeEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1f84fecc2ecac03ba6d8a18588d2f0163930b701
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica el tipo de [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica un *simple* registro (que no contiene nodos secundarios).|  
|**adCollectionRecord**|1|Indica un *colección* registro (que contiene nodos secundarios).|  
|**adRecordUnknown**|-1|Indica que el tipo de este **registro** es desconocido.|  
|**adStructDoc**|2|Indica una clase especial de tipo de *colección* registro que representa COM documentos estructurados.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
