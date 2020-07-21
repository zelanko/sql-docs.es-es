---
title: Puerta de enlace estándar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67551845c0dd8c6a28c0c4bc1c50f54ee8232df1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280078"
---
# <a name="standard-gateway"></a>Puerta de enlace estándar
Una *puerta de enlace* es un elemento de software que hace que un DBMS tenga el mismo aspecto que otro. Es decir, la puerta de enlace acepta la interfaz de programación, la gramática de SQL y el protocolo de flujo de datos de un solo DBMS y lo traduce a la interfaz de programación, la gramática de SQL y el protocolo de flujo de datos del DBMS oculto. Por ejemplo, las aplicaciones escritas para usar Microsoft® SQL Server™ también pueden acceder a los datos de DB2 a través de la puerta de enlace DB2 de micro decisionware; Este producto hace que DB2 tenga el siguiente aspecto SQL Server. Cuando se usan puertas de enlace, se debe escribir una puerta de enlace diferente para cada base de datos de destino.  
  
 Aunque las puertas de enlace están limitadas por las diferencias arquitectónicas entre los DBMS, son un buen candidato para la normalización. Sin embargo, si todos los DBMS están normalizados en la interfaz de programación, la gramática de SQL y el protocolo de flujo de datos de un solo DBMS, cuyo DBMS debe elegirse como el estándar? Sin duda, no es probable que ningún proveedor de DBMS comercial acepte la estandarización en el producto de un competidor. Y si se desarrollan una interfaz de programación estándar, la gramática de SQL y el protocolo de flujo de datos, no se necesita ninguna puerta de enlace.
