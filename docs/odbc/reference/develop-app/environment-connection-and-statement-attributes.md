---
title: Atributos de instrucción, conexión y entorno | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e77be71458eb10e97a82c925d34141a7bcaf1dc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62943008"
---
# <a name="environment-connection-and-statement-attributes"></a>Entorno, conexión y los atributos de instrucción
ODBC define un número de atributos que están asociados con los entornos, las conexiones o las instrucciones.  
  
 Atributos de entorno afectan a todo el entorno, por ejemplo, si está habilitada la agrupación de conexiones. Los atributos de entorno se establecen con **SQLSetEnvAttr** y recuperarse con **SQLGetEnvAttr**.  
  
 Los atributos de conexión afecta a cada conexión individualmente, como la forma de un controlador de esperar al intentar conectarse a un origen de datos antes de agotar el tiempo. Los atributos de conexión se establecen con **SQLSetConnectAttr** y recuperarse con **SQLGetConnectAttr**. Para obtener más información acerca de los atributos de conexión, consulte [los atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Atributos de instrucción afecta a cada instrucción de forma individual, como si se debería ejecutar una instrucción de forma asincrónica. Atributos de instrucción se establecen con **SQLSetStmtAttr** y recuperarse con **SQLGetStmtAttr**. Algunos atributos de instrucción son atributos de solo lectura y no se puede establecer. Por ejemplo, el atributo de instrucción SQL_ATTR_ROW_NUMBER, que se usa para recuperar el número de la fila actual del cursor, es de sólo lectura. Para obtener más información acerca de los atributos de instrucción, consulte [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Además de los atributos definidos por ODBC, un controlador puede definir su propia conexión y los atributos de instrucción. Atributos definidos por el controlador deben registrarse con Open Group para asegurarse de que dos proveedores de controlador no asignación el mismo valor de entero a atributos diferentes, su propiedad. Para obtener más información, consulte [los tipos de datos específicos del controlador, Descriptor tipos, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obtener una lista completa de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). También se describe la mayoría de los atributos en la descripción de la función ODBC que afectan.
