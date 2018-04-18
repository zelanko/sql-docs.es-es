---
title: Diferida campos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47e9d94d3a3f6e39864d27fee1c82f8e69f24b37
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="deferred-fields"></a>Campos aplazados
Los valores de *diferidas campos* no se usan cuando se establecen, pero el controlador guarda las direcciones de las variables de un efecto diferida. Para un descriptor de parámetros de la aplicación, el controlador utiliza el contenido de las variables en el momento de la llamada a **SQLExecDirect** o **SQLExecute**. Para un descriptor de fila de la aplicación, el controlador utiliza el contenido de las variables en el momento de la captura.  
  
 Éstos son campos aplazados:  
  
-   Los campos de un registro de descriptor SQL_DESC_DATA_PTR y SQL_DESC_INDICATOR_PTR.  
  
-   El campo SQL_DESC_OCTET_LENGTH_PTR de un registro de descriptor de la aplicación.  
  
-   En el caso de una captura de varias filas, los campos SQL_DESC_ARRAY_STATUS_PTR y SQL_DESC_ROWS_PROCESSED_PTR de un encabezado de descriptor.  
  
 Cuando se asigna un descriptor de los campos de cada registro del descriptor aplazados tienen inicialmente un valor null. El significado del valor null es como sigue:  
  
-   Si SQL_DESC_ARRAY_STATUS_PTR tiene un valor null, se produce un error en la captura varias filas devolver este componente de la información de diagnóstico de cada fila.  
  
-   Si SQL_DESC_DATA_PTR tiene un valor null, el registro es independiente.  
  
-   Si el campo SQL_DESC_OCTET_LENGTH_PTR de un descartar tiene un valor null, el controlador no devuelve información sobre la longitud de esa columna.  
  
-   Si el campo SQL_DESC_OCTET_LENGTH_PTR de un APD tiene un valor null y el parámetro es una cadena de caracteres, el controlador supone que cadena terminada en null. Para los parámetros dinámicos de salida, un valor null en este campo evita que el controlador devuelve información sobre la longitud. (Si el campo SQL_DESC_TYPE no indica un parámetro de cadena de caracteres, se omite el campo SQL_DESC_OCTET_LENGTH_PTR.)  
  
 La aplicación no debe cancelar la asignación o descartar las variables utilizadas para campos aplazados entre el momento en que asocia a los campos y el momento en el controlador lee o escribe.
