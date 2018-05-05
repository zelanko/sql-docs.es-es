---
title: Longitud de los datos, la longitud de búfer y truncamiento | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20d0e05e9739cbc8382a7a23c58b48084415990c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-length-buffer-length-and-truncation"></a>Longitud de los datos, la longitud de búfer y truncamiento
El *longitud de datos* es la longitud de bytes de los datos tal y como se almacenaría en búfer de datos de la aplicación, no cuando se almacenan en el origen de datos. Esta distinción es importante porque los datos se almacenan a menudo en los diferentes tipos en el búfer de datos que en el origen de datos. Por lo que para los datos que se envían al origen de datos, esto es la longitud de bytes de los datos antes de la conversión al tipo del origen de datos. Para los datos que se va a recuperar del origen de datos, esto es la longitud de bytes de los datos después de la conversión al tipo de búfer de datos y antes de que se realiza cualquier truncamiento.  
  
 Para los datos de longitud fija, como un entero o una estructura de fecha, la longitud de bytes de los datos siempre es el tamaño del tipo de datos. En general, las aplicaciones asignación un búfer de datos que es el tamaño del tipo de datos. Si la aplicación asigna un búfer más pequeño, las consecuencias son indefinidas porque el controlador supone que el búfer de datos es el tamaño del tipo de datos y no trunca los datos caben en un búfer más pequeño. Si la aplicación asigna un búfer mayor, nunca se utiliza el espacio adicional.  
  
 Para los datos de longitud variable, como datos de caracteres o binarios, es importante reconocer que la longitud de bytes de los datos es independiente de y a menudo es diferente de la longitud de bytes del búfer. La relación de estos dos longitudes se describe en el [búferes](../../../odbc/reference/develop-app/buffers.md) sección. Si la longitud de bytes de los datos es mayor que la longitud de bytes del búfer, el controlador trunca los datos capturados a la longitud de bytes del búfer y devuelve SQL_SUCCESS_WITH_INFO con SQLSTATE 01004 (datos truncados). Sin embargo, la longitud de bytes devuelta es la longitud de los datos untruncated.  
  
 Por ejemplo, suponga que una aplicación asigna 50 bytes para un búfer de datos binarios. Si el controlador tiene 10 bytes de datos binarios que se va a devolver, devuelve los 10 bytes en el búfer. La longitud de bytes de los datos es 10, y la longitud de bytes del búfer es 50. Si el controlador tiene 60 bytes de datos binarios que se va a devolver, trunca los datos a 50 bytes, devuelve los bytes en el búfer y devuelve SQL_SUCCESS_WITH_INFO. La longitud de bytes de los datos es de 60 (la longitud antes de truncamiento) y la longitud de bytes del búfer todavía es 50.  
  
 Se crea un registro de diagnóstico para cada columna que se trunca. Dado que requiere tiempo para el controlador cree estos registros y para la aplicación procesarlos, truncamiento puede degradar el rendimiento. Normalmente, una aplicación puede evitar este problema asignando búferes lo suficientemente grandes, aunque esto no sería posible cuando se trabaja con datos de tipo long. Cuando se produce el truncamiento de datos, la aplicación en ocasiones, puede asignar un búfer mayor y volver a obtener los datos; Esto no es cierto en todos los casos. Si se produce un truncamiento al obtener datos con llamadas a **SQLGetData**, la aplicación no necesita llamar a **SQLGetData** para los datos que ya se ha devuelto; para obtener más información, consulte [Introducción Datos de tipo Long](../../../odbc/reference/develop-app/getting-long-data.md).
