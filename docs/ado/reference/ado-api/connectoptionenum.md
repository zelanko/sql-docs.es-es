---
description: ConnectOptionEnum
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
ms.openlocfilehash: 73fb0218b9a4a9437dbe8c103c8496f0a209e9b1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775814"
---
# <a name="connectoptionenum"></a>ConnectOptionEnum
Especifica si el método [Open](./open-method-ado-connection.md) de un objeto [Connection](./connection-object-ado.md) debe devolver una vez establecida la conexión (sincrónicamente) o antes de (de forma asincrónica).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adAsyncConnect**|16|Abre la conexión de forma asincrónica. El evento [ConnectComplete](./connectcomplete-and-disconnect-events-ado.md) se puede usar para determinar si la conexión está disponible.|  
|**adConnectUnspecified**|-1|Predeterminada. Abre la conexión sincrónicamente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectOption. ASYNCCONNECT|  
|AdoEnums. ConnectOption. CONNECTUNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
 [Open (método) (conexión de ADO)](./open-method-ado-connection.md)