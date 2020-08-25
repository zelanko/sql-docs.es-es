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
ms.openlocfilehash: 1c7ea7ccbf1a588458db9e213bfa57837e89898f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776824"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica los atributos de transacción de un objeto de [conexión](./connection-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262 144|Realiza las anulaciones de retención llamando a [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automáticamente una nueva transacción. No todos los proveedores admiten este comportamiento.|  
|**adXactCommitRetaining**|131 072|Realiza la retención de confirmaciones mediante una llamada a [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automáticamente una nueva transacción. No todos los proveedores admiten este comportamiento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. XactAttribute. ABORTRETAINING|  
|AdoEnums. XactAttribute. COMMITRETAINING|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Attributes (ADO)](./attributes-property-ado.md)