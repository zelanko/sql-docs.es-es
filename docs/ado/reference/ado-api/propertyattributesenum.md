---
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: rothja
ms.author: jroth
ms.openlocfilehash: dcb17116d7332e9afb359a7dd47d69cb3eb75df4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759941"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Especifica los atributos de un objeto de [propiedad](../../../ado/reference/ado-api/property-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|Indica que el proveedor no admite la propiedad.|  
|**adPropRequired**|1|Indica que el usuario debe especificar un valor para esta propiedad antes de inicializar el origen de datos.|  
|**adPropOptional**|2|Indica que el usuario no necesita especificar un valor para esta propiedad antes de inicializar el origen de datos.|  
|**adPropRead**|512|Indica que el usuario puede leer la propiedad.|  
|**adPropWrite**|1024|Indica que el usuario puede establecer la propiedad.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. PropertyAttributes. NOTSUPPORTED|  
|AdoEnums. PropertyAttributes. Required|  
|AdoEnums. PropertyAttributes. opcional|  
|AdoEnums. PropertyAttributes. READ|  
|AdoEnums. PropertyAttributes. WRITE|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
