---
description: XactAttributeEnum
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: rothja
ms.author: jroth
ms.openlocfilehash: 2528c9b7a8cf9eb2918983d90e57ac39e6ee989e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441457"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica los atributos de transacción de un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262 144|Realiza las anulaciones de retención llamando a [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automáticamente una nueva transacción. No todos los proveedores admiten este comportamiento.|  
|**adXactCommitRetaining**|131 072|Realiza la retención de confirmaciones mediante una llamada a [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automáticamente una nueva transacción. No todos los proveedores admiten este comportamiento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. XactAttribute. ABORTRETAINING|  
|AdoEnums. XactAttribute. COMMITRETAINING|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
