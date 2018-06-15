---
title: Más | Documentos de Microsoft
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
- PersistFormatEnum
helpviewer_keywords:
- PersistFormatEnum enumeration [ADO]
ms.assetid: ebe1a2ab-e9f1-43a2-8f94-b190c9613d70
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9aa6ce5a4341c85f7763d407b0d39599b24d9441
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280614"
---
# <a name="persistformatenum"></a>Más
Especifica el formato en el que se va a guardar una [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Valor|Descripción|  
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
