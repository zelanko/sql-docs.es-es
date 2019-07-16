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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 819fb89d7f8c43e76ba9260a72fafa68084bf880
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933444"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica si el [abierto](../../../ado/reference/ado-api/open-method-ado-connection.md) método de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) debe devolver el objeto una vez establecida la conexión (sincrónicamente) o antes (asincrónicamente).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Se abre la conexión de forma asincrónica. El [ConnectComplete](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md) evento puede utilizarse para determinar cuándo está disponible la conexión.|  
|**adConnectUnspecified**|-1|Predeterminado: Abre la conexión de forma sincrónica.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectOption.ASYNCCONNECT|  
|AdoEnums.ConnectOption.CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)
