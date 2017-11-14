---
title: "Más | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c981037637b85e23e6b871116291aa8eb607c99
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="persistformatenum"></a>Más
Especifica el formato en el que se va a guardar una [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica el formato de Microsoft Advanced Data TableGram (ADTG).|  
|**adPersistADO**|1|Indica que se utilizará el formato de lenguaje de marcado Extensible (XML) de ADO. Este valor es el mismo que adPersistXML y es incluye por compatibilidad con versiones anteriores.|  
|**adPersistXML**|1|Indica el formato de lenguaje de marcado Extensible (XML).|  
|**adPersistProviderSpecific**|2|Indica que el proveedor guardará el **Recordset** mediante su propio formato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Se aplica a  
 [Save (método)](../../../ado/reference/ado-api/save-method.md)

