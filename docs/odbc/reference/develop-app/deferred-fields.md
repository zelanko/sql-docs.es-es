---
title: Campos diferidos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 094aba353e10ed568e1959b1d655109296507dee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305976"
---
# <a name="deferred-fields"></a>Campos aplazados
Los valores de *los campos diferidos* no se utilizan cuando se establecen, pero el controlador guarda las direcciones de las variables para un efecto diferido. Para un descriptor de parámetro de aplicación, el controlador utiliza el contenido de las variables en el momento de la llamada a **SQLExecDirect** o **SQLExecute**. Para un descriptor de fila de aplicación, el controlador utiliza el contenido de las variables en el momento de la captura.  
  
 Los siguientes son campos diferidos:  
  
-   Los campos SQL_DESC_DATA_PTR y SQL_DESC_INDICATOR_PTR de un registro descriptor.  
  
-   El campo SQL_DESC_OCTET_LENGTH_PTR de un registro descriptor de aplicación.  
  
-   En el caso de una captura de varias filas, el SQL_DESC_ARRAY_STATUS_PTR y SQL_DESC_ROWS_PROCESSED_PTR campos de un encabezado descriptor.  
  
 Cuando se asigna un descriptor, los campos diferidos de cada registro descriptor tienen inicialmente un valor nulo. El significado del valor nulo es el siguiente:  
  
-   Si SQL_DESC_ARRAY_STATUS_PTR tiene un valor nulo, una captura de varias filas no puede devolver este componente de la información de diagnóstico por fila.  
  
-   Si SQL_DESC_DATA_PTR tiene un valor nulo, el registro no está enlazado.  
  
-   Si el campo SQL_DESC_OCTET_LENGTH_PTR de un ARD tiene un valor nulo, el controlador no devuelve información de longitud para esa columna.  
  
-   Si el campo SQL_DESC_OCTET_LENGTH_PTR de un APD tiene un valor nulo y el parámetro es una cadena de caracteres, el controlador supone que la cadena está terminada en null. Para los parámetros dinámicos de salida, un valor nulo en este campo impide que el controlador devuelva información de longitud. (Si el campo SQL_DESC_TYPE no indica un parámetro de cadena de caracteres, se omite el campo SQL_DESC_OCTET_LENGTH_PTR.)  
  
 La aplicación no debe desasignar o descartar variables utilizadas para los campos diferidos entre el momento en que los asocia con los campos y el momento en que el controlador los lee o los escribe.
