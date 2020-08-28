---
description: ConnectPromptEnum
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: rothja
ms.author: jroth
ms.openlocfilehash: 171cc7706cc00b48c3373a0e40d5de221d4d00ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974686"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica si se debe mostrar un cuadro de diálogo para solicitar los parámetros que faltan al abrir una conexión a un origen de datos.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Solicita siempre.|  
|**adPromptComplete**|2|Solicita si se requiere más información.|  
|**adPromptCompleteRequired**|3|Solicita si se requiere más información pero no se permiten parámetros opcionales.|  
|**adPromptNever**|4|Nunca solicita.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectPrompt. ALWAYS|  
|AdoEnums. ConnectPrompt. COMPLETE|  
|AdoEnums. ConnectPrompt. COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. NEVER|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad-dinámica Prompt (ADO)](./prompt-property-dynamic-ado.md)