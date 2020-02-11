---
title: Campos diferidos | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076819"
---
# <a name="deferred-fields"></a>Campos aplazados
Los valores de los *campos diferidos* no se usan cuando se establecen, pero el controlador guarda las direcciones de las variables para un efecto diferido. En el caso de un descriptor de parámetros de aplicación, el controlador utiliza el contenido de las variables en el momento de la llamada a **SQLExecDirect** o **SQLExecute**. En el caso de un descriptor de fila de la aplicación, el controlador utiliza el contenido de las variables en el momento de la captura.  
  
 Los siguientes son campos diferidos:  
  
-   Los campos SQL_DESC_DATA_PTR y SQL_DESC_INDICATOR_PTR de un registro del descriptor.  
  
-   SQL_DESC_OCTET_LENGTH_PTR campo de un registro del descriptor de la aplicación.  
  
-   En el caso de una captura de varias filas, los campos SQL_DESC_ARRAY_STATUS_PTR y SQL_DESC_ROWS_PROCESSED_PTR de un encabezado de descriptor.  
  
 Cuando se asigna un descriptor, los campos diferidos de cada registro del descriptor inicialmente tienen un valor null. El significado del valor NULL es el siguiente:  
  
-   Si SQL_DESC_ARRAY_STATUS_PTR tiene un valor null, una captura de varias filas no puede devolver este componente de la información de diagnóstico por fila.  
  
-   Si SQL_DESC_DATA_PTR tiene un valor null, el registro está desenlazado.  
  
-   Si el SQL_DESC_OCTET_LENGTH_PTR campo de un ARD tiene un valor null, el controlador no devuelve información de longitud para esa columna.  
  
-   Si el SQL_DESC_OCTET_LENGTH_PTR campo de un APD tiene un valor NULL y el parámetro es una cadena de caracteres, el controlador supone que la cadena termina en NULL. En el caso de los parámetros dinámicos de salida, un valor null en este campo impide que el controlador devuelva información de longitud. (Si el campo SQL_DESC_TYPE no indica un parámetro de cadena de caracteres, se omite el campo SQL_DESC_OCTET_LENGTH_PTR).  
  
 La aplicación no debe desasignar ni descartar las variables usadas para los campos diferidos entre el momento en que las asocia con los campos y la hora en que el controlador las lee o las escribe.
