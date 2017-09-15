---
title: ADCPROP_AUTORECALC_ENUM | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f5639a1e86ce6b9e46b3583c8e092e389dfa422e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
Especifica cuándo la [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) proveedor vuelve a calcular las columnas agregadas y calculadas en un objeto Recordset jerárquico.  
  
 Estas constantes sólo se utilizan con la **MSDataShape** proveedor y el **Recordset** "**recálculo automático**" propiedad dinámica, que se hace referencia en el [ADO Índice de propiedades dinámicas](../../../ado/reference/ado-api/ado-dynamic-property-index.md) y documentado en el [servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) o [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentación.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Predeterminado: Vuelve a calcular cada vez que la **MSDataShape** proveedor determina han cambiado los valores que dependen de las columnas calculadas.|  
|**adRecalcUpFront**|0|Calcula sólo al generar inicialmente el jerárquica **conjunto de registros**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.
