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
manager: craigg
ms.openlocfilehash: 195f76043cf65801289d081e497e28a41aff3209
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761443"
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
