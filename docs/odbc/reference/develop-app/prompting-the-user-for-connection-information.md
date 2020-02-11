---
title: Solicitando al usuario información de conexión | Microsoft Docs
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
ms.openlocfilehash: 7dfc63aaa6f162d382d6d8b3c627ff078c76825c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079065"
---
# <a name="prompting-the-user-for-connection-information"></a>Preguntar al usuario información de conexión
Si la aplicación usa **SQLConnect** y necesita preguntar al usuario sobre la información de conexión, como un nombre de usuario y una contraseña, debe hacerlo. Aunque esto permite que la aplicación controle su "aspecto y funcionamiento", puede obligar a la aplicación a contener código específico del controlador. Esto sucede cuando la aplicación necesita solicitar al usuario información de conexión específica del controlador. Esto supone una situación imposible para las aplicaciones genéricas, que están diseñadas para funcionar con todos los controladores, incluidos los controladores que no existen cuando se escribe la aplicación.  
  
 **SQLDriverConnect** puede solicitar al usuario la información de conexión. Por ejemplo, el programa personalizado mencionado anteriormente podría pasar la cadena de conexión siguiente a **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 Después, el controlador podría mostrar un cuadro de diálogo en el que se solicitan los identificadores de usuario y las contraseñas, de forma similar a la siguiente ilustración.  
  
 ![Cuadro de diálogo que solicita al usuario que especifique id. de usuario y contraseñas](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Que el controlador puede solicitar información de conexión es especialmente útil para las aplicaciones genéricas y verticales. Estas aplicaciones no deben contener información específica del controlador y, si se solicita la información necesaria para la información que necesita, se conserva la información de la aplicación. Esto se muestra en los dos ejemplos anteriores. Cuando la aplicación pasa solo el nombre del origen de datos al controlador, la aplicación no contenía ninguna información específica del controlador y, por tanto, no estaba asociada a un controlador determinado. Cuando la aplicación pasa una cadena de conexión completa al controlador, estaba vinculada al controlador que podría interpretar esa cadena.  
  
 Una aplicación genérica podría tardar un paso más y no especificar un origen de datos. Cuando **SQLDriverConnect** recibe una cadena de conexión vacía, el administrador de controladores muestra el siguiente cuadro de diálogo.  
  
 ![Cuadro de diálogo Seleccionar origen de datos](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Una vez que el usuario selecciona un origen de datos, el administrador de controladores crea una cadena de conexión que especifica ese origen de datos y lo pasa al controlador. A continuación, el controlador puede solicitar al usuario cualquier información adicional que necesite.  
  
 Las condiciones en las que el controlador solicita al usuario se controlan mediante la marca *DriverCompletion* . hay opciones para preguntar siempre, preguntar si es necesario o no preguntar nunca. Para obtener una descripción completa de esta marca, vea la descripción de la función [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .
