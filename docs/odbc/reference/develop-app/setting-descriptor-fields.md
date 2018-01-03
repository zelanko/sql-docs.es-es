---
title: Establecer campos de Descriptor | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc02690bd62802f9d356851cd85522328107a707
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="setting-descriptor-fields"></a>Campos de Descriptor de configuración
Para modificar los campos de un descriptor, una aplicación puede llamar a **SQLSetDescField**. Algunos campos son de solo lectura y no se puede establecer. (Consulte la [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) descripción de la función.)  
  
 Campos de registro del descriptor se establecen con un número de registro (*RecNumber*) de tiempo de 1 o superior, se establecen los campos de encabezado de descriptor con un número de registro de 0. Un número de registro de 0 también se usa para establecer los campos de marcador, según la convención de que los marcadores están incluidos en la columna 0. Esto podría dejar a la impresión de que los campos de marcador se encuentran dentro del encabezado de descriptor, pero esto no es el caso. Campos de marcador son distintos de los campos de encabezado.  
  
 Al establecer campos de forma individual, la aplicación debe seguir la secuencia definida en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Establecer algunos campos, el controlador establecer otros campos. Esto garantiza que el descriptor siempre está listo para usar una vez que la aplicación ha especificado un tipo de datos. Cuando la aplicación establece el campo SQL_DESC_TYPE, el controlador comprueba que otros campos que especifican el tipo sean válidos y coherentes.  
  
 Si se produce un error en una llamada de función que establecía un campo descriptor, el contenido del campo descriptor es indefinido después de la llamada de función con errores.
