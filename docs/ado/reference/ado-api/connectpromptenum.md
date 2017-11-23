---
title: ConnectPromptEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ConnectPromptEnum
helpviewer_keywords: ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dbb4f3f854f319d31f91f8e7f0d8a15cf4263495
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica si se debe mostrar un cuadro de diálogo para pedir parámetros que faltan al abrir una conexión a un origen de datos.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Solicita información siempre.|  
|**adPromptComplete**|2|Solicita si se necesita más información.|  
|**adPromptCompleteRequired**|3|Pide confirmación si se necesita más información, pero no se permiten parámetros opcionales.|  
|**adPromptNever**|4|Solicita información nunca.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad-dinámica Prompt (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
