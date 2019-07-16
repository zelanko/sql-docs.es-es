---
title: Aplaza campos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2c229d31941d5cef0da253545cecd7d1496ee4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076819"
---
# <a name="deferred-fields"></a>Campos aplazados
Los valores de *aplazada campos* no se usan cuando se establecen, pero el controlador guarda las direcciones de las variables para un efecto aplazada. Para un descriptor de parámetro de la aplicación, el controlador utiliza el contenido de las variables en el momento de la llamada a **SQLExecDirect** o **SQLExecute**. Para un descriptor de fila de la aplicación, el controlador utiliza el contenido de las variables en el momento de la operación de captura.  
  
 Los siguientes son campos aplazados:  
  
-   Los campos de un registro de descriptor SQL_DESC_DATA_PTR y SQL_DESC_INDICATOR_PTR.  
  
-   El campo SQL_DESC_OCTET_LENGTH_PTR un registro del descriptor de aplicación.  
  
-   En el caso de una captura de varias filas, los campos SQL_DESC_ARRAY_STATUS_PTR y SQL_DESC_ROWS_PROCESSED_PTR de un encabezado de descriptor.  
  
 Cuando se asigna un descriptor, los campos de cada registro de descriptor aplazados inicialmente tienen un valor null. El significado del valor null es como sigue:  
  
-   Si SQL_DESC_ARRAY_STATUS_PTR tiene un valor null, una captura de varias filas no puede devolver este componente de la información de diagnóstico de cada fila.  
  
-   Si SQL_DESC_DATA_PTR tiene un valor null, el registro es independiente.  
  
-   Si el campo SQL_DESC_OCTET_LENGTH_PTR de un descartar tiene un valor null, el controlador no devuelve información de longitud para esa columna.  
  
-   Si el campo SQL_DESC_OCTET_LENGTH_PTR de un APD tiene un valor null y el parámetro es una cadena de caracteres, el controlador supone que cadena terminada en null. Parámetros de salida dinámicas, un valor null en este campo impide que el controlador devolver información de longitud. (Si el campo SQL_DESC_TYPE no indica un parámetro de cadena de caracteres, se omite el campo SQL_DESC_OCTET_LENGTH_PTR.)  
  
 La aplicación no debe desasignar o descartar variables usados en los campos aplazados entre el momento en que asocia a los campos y la hora en que el controlador lee o escribe.
