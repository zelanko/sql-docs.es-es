---
title: RecordTypeEnum | Documentos de Microsoft
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
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c583db7cb8d91090357a26f027478485d087d9f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281224"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica el tipo de [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica un *simple* registro (que no contiene nodos secundarios).|  
|**adCollectionRecord**|1|Indica un *colección* registro (que contiene nodos secundarios).|  
|**adRecordUnknown**|-1|Indica que el tipo de este **registro** es desconocido.|  
|**adStructDoc**|2|Indica una clase especial de tipo de *colección* registro que representa COM documentos estructurados.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
