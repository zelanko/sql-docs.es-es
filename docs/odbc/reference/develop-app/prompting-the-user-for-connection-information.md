---
title: Solicitar al usuario la información de conexión de la red de datos de conexión de la red de datos de la red de datos de la Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b0f120a1076f14f5e67d506e52a446e0a3d4713
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282088"
---
# <a name="prompting-the-user-for-connection-information"></a>Preguntar al usuario información de conexión
Si la aplicación utiliza **SQLConnect** y necesita solicitar al usuario cualquier información de conexión, como un nombre de usuario y una contraseña, debe hacerlo él mismo. Si bien esto permite a la aplicación controlar su "aspecto", podría forzar a la aplicación a contener código específico del controlador. Esto ocurre cuando la aplicación necesita solicitar al usuario información de conexión específica del controlador. Esto presenta una situación imposible para las aplicaciones genéricas, que están diseñadas para trabajar con todos y cada uno de los controladores, incluidos los controladores que no existen cuando se escribe la aplicación.  
  
 **SQLDriverConnect** puede solicitar al usuario información de conexión. Por ejemplo, el programa personalizado mencionado anteriormente podría pasar la siguiente cadena de conexión a **SQLDriverConnect:**  
  
```  
DSN=XYZ Corp;  
```  
  
 A continuación, el controlador puede mostrar un cuadro de diálogo que solicita los ID de usuario y las contraseñas, de forma similar a la siguiente ilustración.  
  
 ![Cuadro de diálogo que solicita al usuario que especifique id. de usuario y contraseñas](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Que el controlador puede solicitar información de conexión es especialmente útil para aplicaciones genéricas y verticales. Estas aplicaciones no deben contener información específica del controlador y tener el identificador del controlador para la información que necesita mantiene esa información fuera de la aplicación. Esto se muestra en los dos ejemplos anteriores. Cuando la aplicación pasó solo el nombre del origen de datos al controlador, la aplicación no contenía ninguna información específica del controlador y, por lo tanto, no estaba vinculada a un controlador determinado. Cuando la aplicación pasó una cadena de conexión completa al controlador, estaba vinculada al controlador que podía interpretar esa cadena.  
  
 Una aplicación genérica podría llevar esto un paso más allá y ni siquiera especificar un origen de datos. Cuando **SQLDriverConnect** recibe una cadena de conexión vacía, el Administrador de controladores muestra el siguiente cuadro de diálogo.  
  
 ![Cuadro de diálogo Seleccionar origen de datos](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Después de que el usuario selecciona un origen de datos, el Administrador de controladores construye una cadena de conexión que especifica ese origen de datos y lo pasa al controlador. A continuación, el controlador puede solicitar al usuario cualquier información adicional que necesite.  
  
 Las condiciones en las que el controlador solicita al usuario se controlan mediante el *DriverCompletion* marca; hay opciones para preguntar siempre, preguntar si es necesario, o nunca preguntar. Para obtener una descripción completa de esta marca, vea la descripción de la función [SQLDriverConnect.](../../../odbc/reference/syntax/sqldriverconnect-function.md)
