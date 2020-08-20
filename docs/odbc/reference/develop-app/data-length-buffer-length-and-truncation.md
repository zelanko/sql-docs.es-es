---
description: Longitud de los datos, la longitud de búfer y truncamiento
title: Longitud de los datos, longitud del búfer y truncamiento | Microsoft Docs
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
ms.openlocfilehash: c9a9651f39c1ff4d2c6dc9b691453fb5354c9e1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465837"
---
# <a name="data-length-buffer-length-and-truncation"></a>Longitud de los datos, la longitud de búfer y truncamiento
La *longitud* de los datos es la longitud de bytes de los datos tal como se almacenaría en el búfer de datos de la aplicación, no como se almacena en el origen de datos. Esta distinción es importante porque los datos suelen almacenarse en tipos diferentes en el búfer de datos que en el origen de datos. Para que los datos se envíen al origen de datos, es la longitud de bytes de los datos antes de la conversión al tipo de origen de datos. Para los datos que se recuperan del origen de datos, es la longitud de bytes de los datos después de la conversión al tipo de búfer de datos y antes de que se realice cualquier truncamiento.  
  
 En el caso de los datos de longitud fija, como un entero o una estructura de fecha, la longitud de bytes de los datos siempre es el tamaño del tipo de datos. En general, las aplicaciones asignan un búfer de datos que es el tamaño del tipo de datos. Si la aplicación asigna un búfer más pequeño, las consecuencias son indefinidas porque el controlador supone que el búfer de datos es el tamaño del tipo de datos y no trunca los datos para caber en un búfer más pequeño. Si la aplicación asigna un búfer mayor, nunca se utiliza el espacio adicional.  
  
 En el caso de los datos de longitud variable, como los datos de caracteres o binarios, es importante reconocer que la longitud de bytes de los datos es independiente y, a menudo, distinta de la longitud de bytes del búfer. La relación de estas dos longitudes se describe en la sección de [búferes](../../../odbc/reference/develop-app/buffers.md) . Si la longitud de bytes de los datos es mayor que la longitud de bytes del búfer, el controlador trunca los datos capturados a la longitud en bytes del búfer y devuelve SQL_SUCCESS_WITH_INFO con SQLSTATE 01004 (datos truncados). Sin embargo, la longitud de bytes devuelta es la longitud de los datos sin truncar.  
  
 Por ejemplo, supongamos que una aplicación asigna 50 bytes para un búfer de datos binarios. Si el controlador tiene 10 bytes de datos binarios que se van a devolver, devuelve los 10 bytes en el búfer. La longitud de bytes de los datos es 10 y la longitud de bytes del búfer es 50. Si el controlador tiene 60 bytes de datos binarios que se van a devolver, trunca los datos en 50 bytes, devuelve los bytes en el búfer y devuelve SQL_SUCCESS_WITH_INFO. La longitud de bytes de los datos es 60 (la longitud antes del truncamiento) y la longitud de bytes del búfer sigue siendo 50.  
  
 Se crea un registro de diagnóstico para cada columna que se trunca. Dado que el controlador tarda en crear estos registros y para que la aplicación los procese, el truncamiento puede reducir el rendimiento. Normalmente, una aplicación puede evitar este problema asignando búferes suficientemente grandes, aunque esto podría no ser posible al trabajar con datos largos. Cuando se produce el truncamiento de datos, la aplicación a veces puede asignar un búfer mayor y volver a capturar los datos. Esto no es cierto en todos los casos. Si se produce un truncamiento mientras se obtienen datos con llamadas a **SQLGetData**, la aplicación no necesita llamar a **SQLGetData** para los datos que ya se han devuelto; para obtener más información, vea [obtener datos de tipo Long](../../../odbc/reference/develop-app/getting-long-data.md).
