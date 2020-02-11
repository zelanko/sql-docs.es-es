---
title: Controladores y aplicaciones compatibles con los estándares | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4980cfe64a5a8e8404c6b5b0bdc8b1aba484f0c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107332"
---
# <a name="standards-compliant-applications-and-drivers"></a>Controladores y aplicaciones compatibles con estándares
Una aplicación o un controlador compatible con los estándares es uno que se ajusta a la especificación del grupo de apertura "Administración de datos: la interfaz de nivel de llamada de SQL (CLI)" y la interfaz de nivel de llamada ISO/IEC 9075-3:1995 (E) (SQL/CLI).  
  
 ODBC *3. x* garantiza las siguientes características:  
  
-   Una aplicación escrita en las especificaciones Open Group e ISO CLI funcionará con un controlador ODBC *3. x* o con un controlador compatible con los estándares cuando se compila con los archivos de encabezado ODBC *3.* x y se vincula con bibliotecas ODBC *3. x* , y cuando obtiene acceso al controlador a través del administrador de controladores ODBC *3. x* .  
  
-   Un controlador escrito en las especificaciones Open Group e ISO CLI funcionará con una aplicación ODBC *3. x* o conforme a los estándares cuando se compila con los archivos de encabezado ODBC *3.* x y se vinculan a las bibliotecas ODBC *3. x* , y cuando la aplicación obtiene acceso al controlador a través del administrador de controladores ODBC *3. x* .  
  
 Los controladores y las aplicaciones conformes a los estándares se compilan con la marca de compilar ODBC_STD.  
  
 Las aplicaciones conformes a los estándares presentan el siguiente comportamiento:  
  
-   Si una aplicación compatible con los estándares llama a **SQLAllocEnv** (que puede producirse porque **SQLAllocEnv** es una función válida en el grupo Open y la CLI ISO), la llamada se asigna a **SQLAllocHandleStd** en tiempo de compilación. Como resultado, en tiempo de ejecución, la aplicación llama a **SQLAllocHandleStd**. Durante el transcurso del procesamiento de esta llamada, el administrador de controladores establece el atributo SQL_ATTR_ODBC_VERSION Environment en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** es equivalente a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** para establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
-   Si una aplicación compatible con los estándares llama a **SQLBindParam** (que puede producirse porque **SQLBindParam** es una función válida en el grupo Open e ISO CLI), el administrador de controladores ODBC *3. x* asigna la llamada a la llamada equivalente en **SQLBindParameter**. (Consulte [asignación de SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) en el Apéndice G: instrucciones del controlador para la compatibilidad con versiones anteriores).  
  
-   Para alinear con la CLI ISO, los archivos de encabezado ODBC *3. x* contienen alias para los tipos de información que se usan en las llamadas a **SQLGetInfo**. Una aplicación compatible con los estándares puede usar estos alias en lugar de los tipos de información de ODBC *3. x* . Para obtener más información, vea el tema siguiente, [archivos de encabezado](../../../odbc/reference/develop-app/header-files.md).  
  
-   Una aplicación compatible con los estándares debe comprobar que todas las características que admite se admiten en el controlador con el que se va a trabajar. Establecer el atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE en SQL_SCROLLABLE y establecer el atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY en SQL_INSENSITIVE o SQL_SENSITIVE son funciones que están disponibles como características opcionales en los estándares pero que no se incluyen en el nivel de núcleo de ODBC *3. x* y, por lo tanto, es posible que no sean compatibles con todos los controladores ODBC *3. x* . Si una aplicación compatible con los estándares utiliza estas capacidades, debe comprobar que el controlador con el que funcionará las admite.
