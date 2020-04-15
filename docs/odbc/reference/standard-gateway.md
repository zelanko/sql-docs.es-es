---
title: Puerta de enlace estándar (Standard Gateway) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280078"
---
# <a name="standard-gateway"></a>Puerta de enlace estándar
Una puerta de *enlace* es una pieza de software que hace que un DBMS se parezca a otro. Es decir, la puerta de enlace acepta la interfaz de programación, la gramática SQL y el protocolo de flujo de datos de un único DBMS y lo traduce a la interfaz de programación, la gramática SQL y el protocolo de flujo de datos del DBMS oculto. Por ejemplo, las aplicaciones escritas para usar Microsoft® SQL Server™ también pueden acceder a los datos de DB2 a través de la puerta de enlace de Micro Decisionware DB2; este producto hace que DB2 se parezca a SQL Server. Cuando se utilizan puertas de enlace, se debe escribir una puerta de enlace diferente para cada base de datos de destino.  
  
 Aunque las puertas de enlace están limitadas por las diferencias arquitectónicas entre los DBMS, son un buen candidato para la estandarización. Sin embargo, si todos los DBMS deben estandarizarse en la interfaz de programación, la gramática SQL y el protocolo de flujo de datos de un único DBMS, cuyo DBMS debe elegirse como estándar? Ciertamente, ningún proveedor comercial de DBMS puede aceptar estandarizar el producto de un competidor. Y si se desarrollan una interfaz de programación estándar, una gramática SQL y un protocolo de flujo de datos, no se necesita ninguna puerta de enlace.
