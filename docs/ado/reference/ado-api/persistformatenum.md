---
description: PersistFormatEnum
title: PersistFormatEnum | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c5730ca6a0d0bae791dce9327e365a9a38a9857f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442737"
---
# <a name="persistformatenum"></a>PersistFormatEnum
Especifica el formato en el que se va a guardar un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Constante|Value|Descripción|  
|--------------|-----------|-----------------|  
|**adPersistADTG**|0|Indica el formato de Microsoft Advanced Data TableGram (ADTG).|  
|**adPersistADO**|1|Indica que se utilizará el propio formato de lenguaje de marcado extensible (XML) de ADO. Este valor es el mismo que el de adPersistXML y se incluye por compatibilidad con versiones anteriores.|  
|**adPersistXML**|1|Indica el formato lenguaje de marcado extensible (XML).|  
|**adPersistProviderSpecific**|2|Indica que el proveedor conservará el **conjunto de registros** con su propio formato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.PersistFormat.ADTG|  
|AdoEnums.PersistFormat.XML|  
  
## <a name="applies-to"></a>Se aplica a  
 [Save (método)](../../../ado/reference/ado-api/save-method.md)
