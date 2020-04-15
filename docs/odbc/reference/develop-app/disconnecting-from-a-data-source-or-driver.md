---
title: Desconectarse de un origen de datos o un controlador ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 154a571bce3a337d539216ce89c32420ab981bd8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300465"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Desconectarse de datos de un origen o el controlador
Cuando una aplicación ha terminado de usar un origen de datos, llama a **SQLDisconnect**. **SQLDisconnect** libera las instrucciones asignadas en la conexión y desconecta el controlador del origen de datos. Devuelve un error si una transacción está en proceso.  
  
 Después de desconectarse, la aplicación puede llamar a **SQLFreeHandle** para liberar la conexión. Después de liberar la conexión, es un error de programación de aplicaciones para usar el identificador de la conexión en una llamada a una función ODBC; hacerlo tiene consecuencias indefinidas, pero probablemente fatales. Cuando **SQLFreeHandle** se llama, el controlador libera la estructura utilizada para almacenar información sobre la conexión.  
  
 La aplicación también puede reutilizar la conexión, ya sea para conectarse a un origen de datos diferente o volver a conectarse al mismo origen de datos. La decisión de permanecer conectado, en lugar de desconectar y volver a conectar más tarde, requiere que el escritor de la aplicación considere los costos relativos de cada opción; tanto la conexión a un origen de datos como el permanecer conectado pueden ser relativamente costosos dependiendo del medio de conexión. Al realizar una compensación correcta, la aplicación también debe hacer suposiciones sobre la probabilidad y el momento de otras operaciones en el mismo origen de datos.
