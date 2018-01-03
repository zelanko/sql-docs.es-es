---
title: ConnectOptionEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ConnectOptionEnum
helpviewer_keywords: ConnectOptionEnum enumeration [ADO]
ms.assetid: bff07eeb-dee3-4e4e-9b2d-d56061ea744d
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 78293f465e1b8a8bfb0195c048bc0e0145c17abc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica si el [abiertos](../../../ado/reference/ado-api/open-method-ado-connection.md) método de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto debe devolver una vez establecida la conexión (sincrónicamente) o antes (asincrónicamente).  
  
|Constante|Valor|Description|  
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
