---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91b4d64095c02fbf3f969248fc78d375a191fe72
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065290"
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
Especifica qué campos se pueden usar para detectar conflictos durante una actualización optimista de una fila del origen de datos con un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
 Utilice estas constantes con la **Recordset** "**criterios de actualización**" propiedad dinámica que se hace referencia en el [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) y documentado en el [ Servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Detecta los conflictos si se ha cambiado cualquier columna de la fila de origen de datos.|  
|**adCriteriaKey**|0|Detecta conflictos si la columna de clave de los datos de origen de fila ha cambiado, lo que significa que se ha eliminado la fila.|  
|**adCriteriaTimeStamp**|3|Detecta conflictos si la marca de tiempo de los datos de origen de fila se ha cambiado, lo que significa que se ha accedido a la fila después de la **Recordset** obtuvo.|  
|**adCriteriaUpdCols**|2|Detecta conflictos si cualquiera de las columnas del origen de datos de la fila que se corresponden con campos actualizados de la **Recordset** han cambiado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
