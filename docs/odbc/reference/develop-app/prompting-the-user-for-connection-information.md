---
title: Preguntar al usuario información de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58df84bf96306a2cfbc0567a3d5f6cb13514a06e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861912"
---
# <a name="prompting-the-user-for-connection-information"></a>Preguntar al usuario información de conexión
Si la aplicación usa **SQLConnect** y debe pedir al usuario información de conexión, por ejemplo, un nombre de usuario y una contraseña, debe hacerlo propio. Aunque esto permite que la aplicación controlar su "aspecto", es posible que obligue a la aplicación para que contenga código específico del controlador. Esto se produce cuando la aplicación debe solicitar al usuario información de conexión específicos del controlador. Esto presenta una situación imposible para las aplicaciones genéricas, que están diseñados para funcionar con todos los controladores, incluidos los controladores que no existen cuando se escribe la aplicación.  
  
 **SQLDriverConnect** puede pedir al usuario información de conexión. Por ejemplo, el programa personalizado que se ha mencionado anteriormente podría pasar la cadena de conexión siguientes para **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 El controlador, a continuación, puede aparecer un cuadro de diálogo que solicita el Id. de usuario y contraseñas, similares a la siguiente ilustración.  
  
 ![Cuadro de diálogo que solicita los identificadores de usuario y contraseñas](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Que el controlador puede solicitar información de conexión es especialmente útil para aplicaciones genéricas y verticales. Estas aplicaciones no deben contener información específica del controlador, y tener el símbolo del sistema de controlador para la información que necesita mantiene esa información fuera de la aplicación. Esto se muestra mediante los dos ejemplos anteriores. Cuando la aplicación pasa sólo el nombre del origen de datos para el controlador, la aplicación no contiene ninguna información específica del controlador y no por lo tanto, se ha asociado a un controlador determinado. Cuando la aplicación pasa una cadena de conexión completa para el controlador, que se ha vinculado al controlador que se podría interpretar esa cadena.  
  
 Una aplicación genérica podría realizar un paso más y ni siquiera especificar un origen de datos. Cuando **SQLDriverConnect** recibe una cadena de conexión vacía, el Administrador de controladores se muestra el cuadro de diálogo siguiente.  
  
 ![Seleccione origen de datos de cuadro de diálogo](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Después de que el usuario selecciona un origen de datos, el Administrador de controladores construye una cadena de conexión especifica ese origen de datos y lo pasa al controlador. El controlador, a continuación, puede pedir al usuario para cualquier información adicional que necesita.  
  
 Las condiciones en las que el controlador solicita al usuario se controlan mediante el *DriverCompletion* marca; hay opciones para Preguntar siempre, símbolo del sistema si es necesario o nunca solicitar. Para obtener una descripción completa de esta marca, vea el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.
