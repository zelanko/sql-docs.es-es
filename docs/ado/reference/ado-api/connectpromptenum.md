---
title: ConnectPromptEnum | Documentos de Microsoft
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
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ae0c2179e321e521a86fdc76e5f8978ab4ab747
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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

