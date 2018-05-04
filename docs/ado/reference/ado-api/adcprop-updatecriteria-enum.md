---
title: ADCPROP_UPDATECRITERIA_ENUM | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a95040a932e35d96a7b2a384da1a910ada118349
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="adcpropupdatecriteriaenum"></a>ADCPROP_UPDATECRITERIA_ENUM
Especifica los campos que se pueden usar para detectar conflictos durante una actualización optimista de una fila del origen de datos con un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
 Utilice estas constantes con la **Recordset** "**criterios de actualización**" propiedad dinámica, que se hace referencia en el [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) y está documentada en el [ Servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentación.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Detecta conflictos si se ha cambiado cualquier columna de la fila de origen de datos.|  
|**adCriteriaKey**|0|Detecta conflictos si la columna de clave de los datos del origen de fila ha cambiado, lo que significa que se ha eliminado la fila.|  
|**adCriteriaTimeStamp**|3|Detecta conflictos si la marca de tiempo de los datos del origen de fila se ha cambiado, lo que significa que se ha accedido a la fila después de la **Recordset** se obtuvo.|  
|**adCriteriaUpdCols**|2|Detecta conflictos si cualquiera de las columnas del origen de datos de la fila que corresponden a los campos actualizados de la **Recordset** han cambiado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|
