---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9434c4cc81e8a94e87a3afceedc1b40d5ece2c29
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696904"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
Especifica si se debe mostrar un cuadro de diálogo para solicitar parámetros que faltan al abrir una conexión a un origen de datos.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|Solicita siempre.|  
|**adPromptComplete**|2|Pregunta si se necesita más información.|  
|**adPromptCompleteRequired**|3|Pregunta si se necesita más información, pero no se permiten los parámetros opcionales.|  
|**adPromptNever**|4|Nunca solicita.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad-dinámica Prompt (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
