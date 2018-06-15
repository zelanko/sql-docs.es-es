---
title: ADCPROP_AUTORECALC_ENUM | Documentos de Microsoft
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
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 760332da1c922c553d326ef583143ba6ac99fde1
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35275184"
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
Especifica cuándo la [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) proveedor vuelve a calcular las columnas agregadas y calculadas en un objeto Recordset jerárquico.  
  
 Estas constantes sólo se utilizan con la **MSDataShape** proveedor y el **Recordset** "**recálculo automático**" propiedad dinámica, que se hace referencia en el [ADO Índice de propiedades dinámicas](../../../ado/reference/ado-api/ado-dynamic-property-index.md) y documentado en el [servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) o [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Predeterminado: Vuelve a calcular cada vez que la **MSDataShape** proveedor determina han cambiado los valores que dependen de las columnas calculadas.|  
|**adRecalcUpFront**|0|Calcula sólo al generar inicialmente el jerárquica **conjunto de registros**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.
