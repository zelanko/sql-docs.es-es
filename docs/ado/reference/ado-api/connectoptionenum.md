---
title: ConnectOptionEnum | Documentos de Microsoft
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
- ConnectOptionEnum
helpviewer_keywords:
- ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae0f4a06d6c4f25d1d4cb0fb71d6b94a57a07cb2
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277194"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica si el [abiertos](../../../ado/reference/ado-api/open-method-ado-connection.md) método de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto debe devolver una vez establecida la conexión (sincrónicamente) o antes (asincrónicamente).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Abre la conexión de forma asincrónica. El [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) evento puede utilizarse para determinar si la conexión está disponible.|  
|**adConnectUnspecified**|-1|Predeterminado: Abre la conexión de forma sincrónica.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
