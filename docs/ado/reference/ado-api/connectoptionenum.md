---
title: ConnectOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
author: rothja
ms.author: jroth
ms.openlocfilehash: fa372f05a80290e907298a0969d9eb9f14355f90
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762606"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica si el método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) de un objeto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) debe devolver una vez establecida la conexión (sincrónicamente) o antes de (de forma asincrónica).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Abre la conexión de forma asincrónica. El evento [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) se puede usar para determinar si la conexión está disponible.|  
|**adConnectUnspecified**|-1|Predeterminada. Abre la conexión sincrónicamente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectOption. ASYNCCONNECT|  
|AdoEnums. ConnectOption. CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
