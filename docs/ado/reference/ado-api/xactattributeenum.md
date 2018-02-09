---
title: XactAttributeEnum | Documentos de Microsoft
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
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c4ffc6f7ad1c7b65a5a6345c459c695409840a1e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica los atributos de transacción de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Realiza anulaciones con retención mediante una llamada a [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) iniciar automáticamente una nueva transacción. No todos los proveedores admiten este comportamiento.|  
|**adXactCommitRetaining**|131072|Realiza confirmaciones con retención mediante una llamada a [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) iniciar automáticamente una nueva transacción. No todos los proveedores admiten este comportamiento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
