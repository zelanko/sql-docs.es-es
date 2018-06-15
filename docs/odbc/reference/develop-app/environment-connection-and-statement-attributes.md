---
title: Entorno, conexión e instrucción atributos | Documentos de Microsoft
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
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b8e3ee068d160269336de15ce1ddef3e7c78d58
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911090"
---
# <a name="environment-connection-and-statement-attributes"></a>Entorno, conexión y los atributos de instrucción
ODBC define el número de atributos que están asociados con los entornos, las conexiones o las instrucciones.  
  
 Atributos de entorno afectan a todo el entorno, por ejemplo, si está habilitada la agrupación de conexiones. Atributos de entorno se establecen con **SQLSetEnvAttr** y se recuperan con **SQLGetEnvAttr**.  
  
 Atributos de conexión afecta a cada conexión de forma individual, como la forma de cuánto tiempo debe esperar un controlador al intentar conectarse a un origen de datos antes de expirar. Atributos de conexión se establecen con **SQLSetConnectAttr** y se recuperan con **SQLGetConnectAttr**. Para obtener más información acerca de los atributos de conexión, vea [atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Atributos de instrucción afecta a cada instrucción de individualmente, por ejemplo, si una instrucción se debe ejecutar de forma asincrónica. Atributos de instrucción se establecen con **SQLSetStmtAttr** y se recuperan con **SQLGetStmtAttr**. Algunos atributos de instrucción son atributos de solo lectura y no se puede establecer. Por ejemplo, el atributo de instrucción SQL_ATTR_ROW_NUMBER, que se utiliza para recuperar el número de la fila actual del cursor, es de sólo lectura. Para obtener más información acerca de los atributos de instrucción, consulte [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Además de los atributos definidos por ODBC, un controlador puede definir su propia conexión y los atributos de instrucción. Atributos definidos por el controlador deben estar registrados con Open Group para asegurarse de que dos proveedores de controlador no asignan el mismo valor de entero a atributos diferentes, propietarios. Para obtener más información, consulte [tipos de datos específicos del controlador, Descriptor de tipos, información de tipos, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obtener una lista completa de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). También se describe la mayoría de los atributos en la descripción de la función ODBC que afectan a.
