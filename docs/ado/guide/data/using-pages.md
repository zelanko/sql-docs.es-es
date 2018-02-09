---
title: "Utilizando páginas | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd893e19c1ab5ac5a4dd657ce61ef76295f2b188
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="using-pages"></a>Usando las páginas.
Use la **PageCount** propiedad para determinar cuántas páginas de datos están en el **Recordset** objeto. *Páginas* son grupos de registros cuyo tamaño es igual a la **PageSize** configuración de la propiedad. Incluso aunque la última página esté incompleta porque hay menos registros que el **PageSize** valor, cuenta como una página adicional en el **PageCount** valor. Si el **Recordset** objeto no admite esta propiedad, **PageCount** será -1 para indicar que la **PageCount** no es posible determinar.  
  
 Use la **PageSize** propiedad para determinar cuántos registros componen una página lógica de datos. Establecer un tamaño de página le permite usar la **AbsolutePage** propiedad para desplazarse al primer registro de una página determinada. Esto es útil en escenarios de servidor Web cuando desea permitir al usuario desplazarse por los datos, ve un cierto número de registros a la vez.  
  
 Esta propiedad puede establecerse en cualquier momento y su valor se usará para calcular la ubicación del primer registro de una página determinada.  
  
 Use la **AbsolutePage** propiedad para identificar el número de página en el que se encuentra el registro actual. Una vez más, el proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
 **AbsolutePage** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro de la **conjunto de registros**. Establezca esta propiedad para desplazarse al primer registro de una página determinada. Obtener el número total de páginas de la **PageCount** propiedad.
