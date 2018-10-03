---
title: Controladores y aplicaciones compatibles con estándares | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8937c2b9c80209975d03963acb19ab5da9c99e39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811343"
---
# <a name="standards-compliant-applications-and-drivers"></a>Controladores y aplicaciones compatibles con estándares
Un controlador o aplicación compatible con los estándares es aquella que se ajusta a la especificación de CAE grupo Open "datos de administración: SQL nivel de llamada interfaz (CLI)" y la norma ISO/IEC 9075-3:1995 interfaz de nivel de llamada (E) (SQL/CLI).  
  
 ODBC 3 *.x* garantiza las siguientes características:  
  
-   Una aplicación creada a las especificaciones de Open Group y ISO CLI funcionará con una aplicación ODBC 3 *.x* controlador o un controlador compatible con los estándares cuando se compila con ODBC 3 *.x* archivos de encabezado y enlazan con ODBC 3 *.x* bibliotecas, y cuando obtiene acceso al controlador a través de la ODBC 3 *.x* Administrador de controladores.  
  
-   Un controlador que se escriben en las especificaciones de Open Group y ISO CLI funcionará con una aplicación ODBC 3 *.x* aplicación o una aplicación estándar cuando se compila con ODBC 3 *.x* archivos de encabezado y vinculado con ODBC 3 *.x* bibliotecas, y cuando la aplicación obtiene acceso al controlador a través de los 3 ODBC *.x* Administrador de controladores.  
  
 Controladores y aplicaciones compatibles con los estándares se compilan con la marca de compilación ODBC_STD.  
  
 Aplicaciones compatibles con los estándares de presentan el siguiente comportamiento:  
  
-   Si llama una aplicación compatible con los estándares **SQLAllocEnv** (lo que puede producirse porque **SQLAllocEnv** es una función válida en el grupo de abierto y ISO CLI), la llamada se asigna a  **SQLAllocHandleStd** en tiempo de compilación. Como resultado, en tiempo de ejecución llama la aplicación **SQLAllocHandleStd**. Durante el transcurso de procesamiento de esta llamada, el Administrador de controladores establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** es equivalente a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
-   Si llama una aplicación compatible con los estándares **SQLBindParam** (lo que puede producirse porque **SQLBindParam** es una función válida en el grupo de abierto y ISO CLI), el 3 de ODBC *.x* Administrador de controladores se asigna la llamada a la llamada equivalente en **SQLBindParameter**. (Consulte [asignación de SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md) en Apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.)  
  
-   Para alinear con la CLI de ISO, el 3 de ODBC *.x* archivos de encabezado contienen un alias para los tipos de información que se usa en llamadas a **SQLGetInfo**. Una aplicación compatible con los estándares puede usar estos alias en lugar de los 3 ODBC *.x* tipos de información. Para obtener más información, vea el tema siguiente, [archivos de encabezado](../../../odbc/reference/develop-app/header-files.md).  
  
-   Una aplicación compatible con los estándares debe comprobar que se admiten todas las características que admite en el controlador que funcione con. Establecer el atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE y configuración del atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE o SQL_SENSITIVE son funciones que están disponibles como características opcionales en los estándares pero no se incluyen en ODBC 3 *.x* Core nivel y, por tanto, puede no ser compatibles con todos los ODBC 3 *.x* controladores. Si una aplicación compatible con los estándares utiliza estas capacidades, debe comprobar que es compatible con el controlador que funcionará con ellos.
