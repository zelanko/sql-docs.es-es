---
title: PropertyAttributesEnum | Documentos de Microsoft
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
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31260a4336954a2efa0cf001d244b7ad7ff7d6a0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280804"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Especifica los atributos de un [propiedad](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
|Constante|Valor|Descripción|  
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
