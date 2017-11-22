---
title: PropertyAttributesEnum | Documentos de Microsoft
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
f1_keywords: PropertyAttributesEnum
helpviewer_keywords: PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 853e63dcd520ab45a26f98091a3e48a816350d0b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Especifica los atributos de un [propiedad](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|Indica que la propiedad no es compatible con el proveedor.|  
|**adPropRequired**|1|Indica que el usuario debe especificar un valor para esta propiedad antes de que se inicialice el origen de datos.|  
|**adPropOptional**|2|Indica que el usuario no necesita especificar un valor para esta propiedad antes de que se inicialice el origen de datos.|  
|**adPropRead**|512|Indica que el usuario puede leer la propiedad.|  
|**adPropWrite**|1024|Indica que el usuario puede establecer la propiedad.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
