---
title: Longitud de los datos, longitud del búfer y truncamiento ( Data Length, Buffer Length, and Truncation) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e7b8d1e60cd83594509c2ab5cbc24e04546eca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305239"
---
# <a name="data-length-buffer-length-and-truncation"></a>Longitud de los datos, la longitud de búfer y truncamiento
La longitud de *los datos* es la longitud de bytes de los datos, ya que se almacenarían en el búfer de datos de la aplicación, no como se almacenan en el origen de datos. Esta distinción es importante porque los datos a menudo se almacenan en tipos diferentes en el búfer de datos que en el origen de datos. Por lo tanto, para los datos que se envían al origen de datos, esta es la longitud de bytes de los datos antes de la conversión al tipo del origen de datos. Para los datos que se recuperan del origen de datos, esta es la longitud de bytes de los datos después de la conversión al tipo del búfer de datos y antes de realizar cualquier truncamiento.  
  
 Para los datos de longitud fija, como un entero o una estructura de fecha, la longitud de bytes de los datos siempre es el tamaño del tipo de datos. En general, las aplicaciones asignan un búfer de datos que es el tamaño del tipo de datos. Si la aplicación asigna un búfer más pequeño, las consecuencias son indefinidas porque el controlador asume que el búfer de datos es el tamaño del tipo de datos y no trunca los datos para que quepan en un búfer más pequeño. Si la aplicación asigna un búfer más grande, nunca se utiliza el espacio adicional.  
  
 Para los datos de longitud variable, como datos binarios o de caracteres, es importante reconocer que la longitud de bytes de los datos es independiente y, a menudo, diferente de la longitud de bytes del búfer. La relación de estas dos longitudes se describe en la sección [Zonas de influencia.](../../../odbc/reference/develop-app/buffers.md) Si la longitud de bytes de los datos es mayor que la longitud de bytes del búfer, el controlador trunca los datos capturados a la longitud de bytes del búfer y devuelve SQL_SUCCESS_WITH_INFO con SQLSTATE 01004 (datos truncados). Sin embargo, la longitud de bytes devuelta es la longitud de los datos no truncados.  
  
 Por ejemplo, supongamos que una aplicación asigna 50 bytes para un búfer de datos binarios. Si el controlador tiene 10 bytes de datos binarios para devolver, devuelve esos 10 bytes en el búfer. La longitud de bytes de los datos es 10 y la longitud de bytes del búfer es 50. Si el controlador tiene 60 bytes de datos binarios para devolver, trunca los datos a 50 bytes, devuelve esos bytes en el búfer y devuelve SQL_SUCCESS_WITH_INFO. La longitud de bytes de los datos es 60 (la longitud antes del truncamiento) y la longitud de bytes del búfer sigue siendo 50.  
  
 Se crea un registro de diagnóstico para cada columna que se trunca. Dado que el controlador tarda tiempo en crear estos registros y para que la aplicación los procese, el truncamiento puede degradar el rendimiento. Normalmente, una aplicación puede evitar este problema asignando búferes lo suficientemente grandes, aunque esto podría no ser posible cuando se trabaja con datos largos. Cuando se produce el truncamiento de datos, la aplicación a veces puede asignar un búfer más grande y volver a capturar los datos; esto no es cierto en todos los casos. Si se produce un truncamiento al obtener datos con llamadas a **SQLGetData**, la aplicación no necesita llamar a **SQLGetData** para los datos que ya se han devuelto; Para obtener más información, consulte [Obtención de datos largos](../../../odbc/reference/develop-app/getting-long-data.md).
