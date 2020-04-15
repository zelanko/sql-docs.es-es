---
title: Atributos de entorno, conexión e instrucción ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86cecaf0b82c7b6d15b3f37262507d2cff0c3c10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300935"
---
# <a name="environment-connection-and-statement-attributes"></a>Entorno, conexión y los atributos de instrucción
ODBC define una serie de atributos asociados a entornos, conexiones o instrucciones.  
  
 Los atributos de entorno afectan a todo el entorno, como si la agrupación de conexiones está habilitada. Los atributos de entorno se establecen con **SQLSetEnvAttr** y se recuperan con **SQLGetEnvAttr**.  
  
 Los atributos de conexión afectan a cada conexión individualmente, como el tiempo que un controlador debe esperar mientras intenta conectarse a un origen de datos antes de agotar el tiempo de espera. Los atributos de conexión se establecen con **SQLSetConnectAttr** y se recuperan con **SQLGetConnectAttr**. Para obtener más información acerca de los atributos de conexión, consulte [Atributos](../../../odbc/reference/develop-app/connection-attributes.md)de conexión .  
  
 Los atributos de instrucción afectan a cada instrucción individualmente, como si una instrucción debe ejecutarse de forma asincrónica. Los atributos de instrucción se establecen con **SQLSetStmtAttr** y se recuperan con **SQLGetStmtAttr**. Algunos atributos de instrucción son atributos de solo lectura y no se pueden establecer. Por ejemplo, el atributo de instrucción SQL_ATTR_ROW_NUMBER, que se utiliza para recuperar el número de la fila actual en el cursor, es de solo lectura. Para obtener más información acerca de los atributos de instrucción, vea Atributos de [instrucción](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Además de los atributos definidos por ODBC, un controlador puede definir sus propios atributos de conexión e instrucción. Los atributos definidos por el controlador deben registrarse en Open Group para asegurarse de que dos proveedores de controladores no asignen el mismo valor entero a atributos propietarios diferentes. Para obtener más información, vea [Tipos de datos específicos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)del controlador, Tipos de descriptor, Tipos de información, Tipos de diagnóstico y Atributos .  
  
 Para obtener una lista completa de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). La mayoría de los atributos también se describen en la descripción de la función ODBC que afectan.
