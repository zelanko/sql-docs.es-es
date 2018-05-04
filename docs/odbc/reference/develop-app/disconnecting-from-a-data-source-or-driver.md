---
title: Desconectarse de datos de un origen o el controlador | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c99a2fb7c441c6de2a229895a1a68d68e9240c7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Desconectarse de datos de un origen o el controlador
Cuando una aplicación ha terminado de usar un origen de datos, se llama a **SQLDisconnect**. **SQLDisconnect** libera las instrucciones que se asignan en la conexión y desconecta el controlador del origen de datos. Devuelve un error si una transacción está en curso.  
  
 Después de desconectarse, la aplicación puede llamar a **SQLFreeHandle** para liberar la conexión. Después de liberar la conexión, es un error de programación de aplicaciones para usar el identificador de la conexión en una llamada a una función ODBC; al hacerlo de modo que tiene consecuencias no definidas, pero probablemente irrecuperables. Cuando **SQLFreeHandle** se llama, las versiones de controlador la estructura que se utiliza para almacenar información acerca de la conexión.  
  
 La aplicación también puede reutilizar la conexión, ya sea para conectarse a un origen de datos diferente o volver a conectarse al mismo origen de datos. La decisión de seguir conectado, en lugar de desconectarse y volver a conectar más tarde, requiere que el escritor de la aplicación, tenga en cuenta los costos relativos de cada opción; conectarse a un origen de datos tanto permanecen conectados pueden ser relativamente costosos dependiendo del medio de conexión. Para realizar un equilibrio correcto, la aplicación debe hacer también suposiciones sobre la probabilidad y temporización de otras operaciones en el mismo origen de datos.
