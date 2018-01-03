---
title: "Puerta de enlace estándar | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e70ef86e0fce41e73cee16074cdfcd6a97177ba7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="standard-gateway"></a>Puerta de enlace estándar
A *puerta de enlace* es un fragmento de software que hace que un DBMS que se parezca a otro. Es decir, la puerta de enlace acepta la interfaz de programación, la gramática SQL y protocolo de un DBMS único de flujo de datos y lo convierte a la interfaz de programación, gramática SQL, y protocolo del DBMS oculto de flujo de datos. Por ejemplo, las aplicaciones escritas para usar Microsoft® SQL Server™ pueden también tener acceso a datos de DB2 a través de la puerta de enlace de Micro Decisionware DB2; Este producto hace DB2 que se parezca a SQL Server. Si se usan las puertas de enlace, se debe escribir una puerta de enlace diferente para cada base de datos de destino.  
  
 Aunque las puertas de enlace están limitados por las diferencias arquitectónicas entre DBMS, son un buen candidato para la estandarización. ¿Sin embargo, si todos los DBMS son estandarizar en la interfaz de programación, gramática de SQL y datos de protocolo de flujo de un sola DBMS, cuyo DBMS es elegirse como el estándar? Por supuesto, ningún proveedor DBMS comercial es probable que acepta estandarizar los productos de la competencia. Y si se ha desarrollado una interfaz de programación estándar, la gramática de SQL y el protocolo de flujo de datos, no es necesaria ninguna puerta de enlace.
