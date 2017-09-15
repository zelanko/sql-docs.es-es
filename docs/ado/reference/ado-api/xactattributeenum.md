---
title: XactAttributeEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b150737eb6323e124569193df7b10e52ac08668f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica los atributos de transacción de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
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
