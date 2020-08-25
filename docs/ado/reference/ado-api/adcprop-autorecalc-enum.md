---
description: ADCPROP_AUTORECALC_ENUM
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7500fd42ef02b974989488b70e668933aaa00cab
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88760270"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
Especifica cuándo el proveedor [MSDataShape](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) vuelve a calcular las columnas agregadas y calculadas en un conjunto de registros jerárquico.  
  
 Estas constantes solo se usan con el proveedor **MSDataShape** y la propiedad dinámica de **conjunto de registros** "**auto Calc**", a la que se hace referencia en el [Índice de propiedades dinámicas de ADO](./ado-dynamic-property-index.md) y se documentan en el servicio [de cursor de Microsoft para OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) o en el [servicio de forma de datos de Microsoft para OLE DB](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentación.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Predeterminada. Vuelve a calcular cada vez que el proveedor **MSDataShape** determina los valores de los que dependen las columnas calculadas.|  
|**adRecalcUpFront**|0|Calcula solo cuando se compila inicialmente el conjunto de **registros**jerárquico.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Estas constantes no tienen equivalentes de ADO/WFC.