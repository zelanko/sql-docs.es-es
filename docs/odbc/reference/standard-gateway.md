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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70a558b065765dd9f8c0895345959e8aa22ebfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232093"
---
# <a name="standard-gateway"></a>Puerta de enlace estándar
Un *puerta de enlace* es un componente de software que hace que un sistema DBMS sea similar a otro. Es decir, la puerta de enlace acepta la interfaz de programación, la gramática de SQL y un DBMS único protocolo de flujo de datos y lo traduce a la interfaz de programación, gramática de SQL, y protocolo del DBMS ocultado la secuencia de datos. Por ejemplo, las aplicaciones escritas para usar Microsoft® SQL Server™ también pueden acceder a datos de DB2 a través de la puerta de enlace de Micro Decisionware DB2; Este producto hace que DB2 sea similar a SQL Server. Cuando se usan las puertas de enlace, otra puerta de enlace debe estar escrita para cada base de datos de destino.  
  
 Aunque las puertas de enlace están limitados por las diferencias arquitectónicas entre DBMS, son un buen candidato para la estandarización. ¿Sin embargo, si todos los DBMS son estandarizar en la interfaz de programación, gramática de SQL y datos de protocolo de secuencia de un DBMS único, cuyo DBMS es elegirse como el estándar? Ciertamente ningún proveedor DBMS comercial es probable que acepta estandarizar en productos de la competencia. Y si se ha desarrollado una interfaz de programación estándar, la gramática SQL y protocolo de transmisión de datos, no es necesaria ninguna puerta de enlace.
