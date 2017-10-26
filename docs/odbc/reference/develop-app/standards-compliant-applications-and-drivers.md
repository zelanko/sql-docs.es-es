---
title: "Controladores y aplicaciones compatibles con los estándares | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standards-compliant applications and drivers [ODBC]
- ODBC drivers [ODBC], standards-compliant
- application features are standards-compliant [ODBC]
ms.assetid: a1145c4c-3094-4f3f-8cc2-e6bb1a930ab1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1aba299d163aaf9ec14d86740e5d8aa91ddb7b3b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="standards-compliant-applications-and-drivers"></a>Controladores y aplicaciones compatibles con estándares
Una aplicación compatible con los estándares o el controlador es aquella que se ajusta a las especificaciones de CAE grupo Open "datos de administración: SQL nivel de llamada Interface (CLI)" y la norma ISO/IEC 9075-3:1995 interfaz de nivel de llamada (E) (SQL/CLI).  
  
 ODBC 3*.x* garantiza las siguientes características:  
  
-   Una aplicación escrita a las especificaciones de Open Group y ISO CLI funcionará con una aplicación ODBC 3*.x* controlador o un controlador compatible con los estándares cuando se compila con ODBC 3*.x* archivos de encabezado y vincular a ODBC 3*.x* bibliotecas, y cuando obtiene acceso al controlador a través de ODBC 3*.x* el Administrador de controladores.  
  
-   Un controlador que se escriben en las especificaciones de Open Group y ISO CLI funcionará con una aplicación ODBC 3*.x* aplicación o una aplicación compatible con los estándares cuando se compila con ODBC 3*.x* archivos de encabezado y vincular con ODBC 3*.x* bibliotecas, y cuando la aplicación obtiene acceso al controlador a través de ODBC 3*.x* el Administrador de controladores.  
  
 Controladores y aplicaciones compatibles con los estándares se compilan con la marca de compilación ODBC_STD.  
  
 Compatible con los estándares aplicaciones presentan el siguiente comportamiento:  
  
-   Si llama a una aplicación compatible con los estándares **SQLAllocEnv** (lo que puede producirse porque **SQLAllocEnv** es una función válida en el Open Group y ISO CLI), la llamada se asigna a ** SQLAllocHandleStd** en tiempo de compilación. Como resultado, en tiempo de ejecución, la aplicación llama **SQLAllocHandleStd**. En el transcurso de procesaba esta llamada, el Administrador de controladores establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** equivale a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
-   Si llama a una aplicación compatible con los estándares **SQLBindParam** (lo que puede producirse porque **SQLBindParam** es una función válida en el Open Group y ISO CLI), ODBC 3*.x* El Administrador de controladores se asigna la llamada a la llamada equivalente en **SQLBindParameter**. (Consulte [SQLBindParam asignación](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.)  
  
-   Para alinear con la CLI de ISO, ODBC 3*.x* archivos de encabezado contienen alias para tipos de información que se utilizan en las llamadas a **SQLGetInfo**. Una aplicación compatible con los estándares puede utilizar estos alias en lugar de ODBC 3*.x* tipos de información. Para obtener más información, vea el tema siguiente, [archivos de encabezado](../../../odbc/reference/develop-app/header-files.md).  
  
-   Una aplicación compatible con los estándares debe comprobar que todas las características que admite son compatibles con el controlador que funcione con. Establecer el atributo de instrucción de SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE y estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE o SQL_SENSITIVE son funciones que están disponibles como características opcionales en las normas pero no se incluyen en ODBC 3*.x* Core nivel y, por tanto, podría no ser compatibles con todos los ODBC 3*.x* controladores. Si una aplicación compatible con los estándares utiliza estas capacidades, debe comprobar que es compatible con el controlador que funcionará con ellos.

