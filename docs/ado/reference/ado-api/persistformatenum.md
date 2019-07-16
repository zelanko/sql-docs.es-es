---
title: Más | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a26fd370e80cb288ee62b0fc53ed6670300172e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917611"
---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica el formato en el que se va a guardar un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica el formato Advanced Data TableGram (ADTG) de Microsoft.|  
|**adPersistADO**|1|Indica que se usará el formato de lenguaje de marcado Extensible (XML) de ADO. Este valor es el mismo que adPersistXML y es incluye por compatibilidad con versiones anteriores.|  
|**adPersistXML**|1|Indica el formato de lenguaje de marcado Extensible (XML).|  
|**adPersistProviderSpecific**|2|Indica que el proveedor se conservará el **Recordset** mediante su propio formato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Se aplica a  
 [Save (método)](../../../ado/reference/ado-api/save-method.md)
