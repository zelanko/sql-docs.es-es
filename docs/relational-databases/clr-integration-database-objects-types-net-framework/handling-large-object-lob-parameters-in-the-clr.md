---
title: "Administrar parámetros de objetos grandes (LOB) en el CLR | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c9692632501eec31e517fb1bade2b3810c18c2b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Administrar parámetros de objetos grandes (LOB) en CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Use **SqlBytes** y **SqlChars** para pasar el tipo binario de objetos grandes (LOB) (**varbinary (max)**) y tipo de carácter LOB (**nvarchar (max)**) parámetros, respectivamente. Estos tipos permiten la transmisión por secuencias de los valores LOB de la base de datos a la rutina de Common Language Runtime (CLR), en lugar de copiar el valor completo en el espacio administrado. **SqlBinary** y **SqlString** debe utilizarse solo para los valores de cadena de caracteres y binarios pequeños.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
