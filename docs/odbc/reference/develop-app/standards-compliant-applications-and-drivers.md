---
title: Aplicaciones y controladores que cumplen con las normas Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4daf2e777b20b1b84c090757d0d84796a4cae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299722"
---
# <a name="standards-compliant-applications-and-drivers"></a>Controladores y aplicaciones compatibles con estándares
Una aplicación o controlador compatible con estándares es aquel que se ajusta a la especificación CAE de grupo abierto "Administración de datos: interfaz de nivel de llamada (CLI) DE SQL y la interfaz de nivel de llamada (SQL/CLI) ISO/IEC 9075-3:1995 (E).  
  
 ODBC *3.x* garantiza las siguientes características:  
  
-   Una aplicación escrita en las especificaciones de Open Group e ISO CLI funcionará con un controlador ODBC *3.x* o un controlador compatible con estándares cuando se compila con los archivos de encabezado ODBC *3.x* y se vincula con bibliotecas ODBC *3.x* y cuando obtiene acceso al controlador a través del Administrador de controladores ODBC *3.x.*  
  
-   Un controlador escrito en las especificaciones de Open Group e ISO CLI funcionará con una aplicación ODBC *3.x* o una aplicación compatible con estándares cuando se compila con los archivos de encabezado ODBC *3.x* y se vincula con bibliotecas ODBC *3.x* y cuando la aplicación obtiene acceso al controlador a través del Administrador de controladores ODBC *3.x.*  
  
 Las aplicaciones y controladores compatibles con estándares se compilan con la marca de compilación ODBC_STD.  
  
 Las aplicaciones conformes a los estándares presentan el siguiente comportamiento:  
  
-   Si una aplicación compatible con estándares llama a **SQLAllocEnv** (que puede producirse porque **SQLAllocEnv** es una función válida en el grupo abierto y la CLI de ISO), la llamada se asigna a **SQLAllocHandleStd** en tiempo de compilación. Como resultado, en tiempo de ejecución, la aplicación llama a **SQLAllocHandleStd**. Durante el procesamiento de esta llamada, el Administrador de controladores establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** es equivalente a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** para establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
-   Si una aplicación compatible con estándares llama a **SQLBindParam** (que puede producirse porque **SQLBindParam** es una función válida en el grupo abierto y la CLI de ISO), el Administrador de controladores ODBC *3.x* asigna la llamada a la llamada equivalente en **SQLBindParameter**. (Consulte Asignación de [SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) en el Apéndice G: Directrices del controlador para la compatibilidad con versiones anteriores.)  
  
-   Para alinearse con la CLI de ISO, los archivos de encabezado ODBC *3.x* contienen alias para los tipos de información utilizados en las llamadas a **SQLGetInfo**. Una aplicación compatible con estándares puede usar estos alias en lugar de los tipos de información ODBC *3.x.* Para obtener más información, consulte el tema siguiente, Archivos de [encabezado](../../../odbc/reference/develop-app/header-files.md).  
  
-   Una aplicación compatible con estándares debe comprobar que todas las características que admite son compatibles con el controlador con el que trabajará. Establecer el atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE en SQL_SCROLLABLE y establecer el atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY en SQL_INSENSITIVE o SQL_SENSITIVE son capacidades que están disponibles como características opcionales en los estándares, pero no se incluyen en el nivel de núcleo ODBC *3.x* y, por lo tanto, es posible que no sean compatibles con todos los controladores ODBC *3.x.* Si una aplicación compatible con estándares usa estas capacidades, debe comprobar que el controlador con el que trabajará las admite.
