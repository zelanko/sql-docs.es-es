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
ms.openlocfilehash: 4606b4345cc52d1371649449890400e01dbc5f51
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114350"
---
# <a name="environment-connection-and-statement-attributes"></a>Entorno, conexión y los atributos de instrucción
ODBC define una serie de atributos que están asociados a entornos, conexiones o instrucciones.  
  
 Los atributos de entorno afectan a todo el entorno, por ejemplo, si está habilitada la agrupación de conexiones. Los atributos de entorno se establecen con **SQLSetEnvAttr** y se recuperan con **SQLGetEnvAttr**.  
  
 Los atributos de conexión afectan individualmente a cada conexión, por ejemplo, cuánto tiempo debe esperar un controlador mientras intenta conectarse a un origen de datos antes de que se agote el tiempo de espera. Los atributos de conexión se establecen con **SQLSetConnectAttr** y se recuperan con **SQLGetConnectAttr**. Para obtener más información sobre los atributos de conexión, consulte [atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Los atributos de instrucción afectan individualmente a cada instrucción, por ejemplo, si una instrucción se debe ejecutar de forma asincrónica. Los atributos de instrucción se establecen con **SQLSetStmtAttr** y se recuperan con **SQLGetStmtAttr**. Algunos atributos de instrucción son atributos de solo lectura y no se pueden establecer. Por ejemplo, el atributo de instrucción SQL_ATTR_ROW_NUMBER, que se usa para recuperar el número de la fila actual del cursor, es de solo lectura. Para obtener más información sobre los atributos de instrucción, vea [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Además de los atributos definidos por ODBC, un controlador puede definir sus propios atributos de conexión y de instrucción. Los atributos definidos por el controlador deben registrarse con Open Group para asegurarse de que dos proveedores de controladores no asignan el mismo valor entero a atributos de propiedad diferentes. Para obtener más información, vea [tipos de datos específicos del controlador, tipos de descriptores, tipos de información, tipos de diagnóstico y atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obtener una lista completa de los atributos, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). La mayoría de los atributos también se describen en la descripción de la función ODBC a la que afectan.
