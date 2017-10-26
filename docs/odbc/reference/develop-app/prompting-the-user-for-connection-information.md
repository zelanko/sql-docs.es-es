---
title: "Preguntar al usuario información de conexión | Documentos de Microsoft"
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b1ee296ea292be7287c2cd4a8e93c9e33cb04bb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="prompting-the-user-for-connection-information"></a>Preguntar al usuario información de conexión
Si la aplicación utiliza **SQLConnect** y debe pedir al usuario ninguna información de conexión, como un nombre de usuario y una contraseña, debe hacerlo propio. Mientras que esto permite que la aplicación controlar su "apariencia y funcionamiento", se puede forzar a la aplicación para que contenga código específico del controlador. Esto se produce cuando la aplicación debe solicitar al usuario información de conexión específicos del controlador. Esto presenta una situación posible para las aplicaciones genéricas, que están diseñados para trabajar con todos los controladores, incluidos los controladores que no existen cuando se escribe la aplicación.  
  
 **SQLDriverConnect** puede pedir al usuario información de conexión. Por ejemplo, el programa personalizado que se ha mencionado anteriormente podría pasar la cadena de conexión siguiente a **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 El controlador, a continuación, podría mostrar un cuadro de diálogo que solicita el Id. de usuario y contraseñas, similares a la siguiente ilustración.  
  
 ![Cuadro de diálogo que pide Id. de usuario y contraseñas](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Que el controlador puede solicitar información de conexión es especialmente útil para aplicaciones verticales y no genéricos. Estas aplicaciones no deben contener información específica del controlador, y tener el indicador de controlador de la información que necesita mantiene esa información fuera de la aplicación. Esto se muestra con los dos ejemplos anteriores. Cuando la aplicación pasa sólo el nombre del origen de datos para el controlador, la aplicación no contenía ninguna información específica del controlador y, por tanto, no estuviera asociada a un controlador específico. Cuando la aplicación pasa una cadena de conexión completa para el controlador, se ha asociado al controlador que podría interpretar esa cadena.  
  
 Una aplicación genérica podría tardar un paso más y ni siquiera especificar un origen de datos. Cuando **SQLDriverConnect** recibe una cadena de conexión vacía, el Administrador de controladores muestra el cuadro de diálogo siguiente.  
  
 ![Cuadro de diálogo Selección de origen de datos](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Cuando el usuario selecciona un origen de datos, el Administrador de controladores construye una cadena de conexión especifica ese origen de datos y lo pasa al controlador. El controlador, a continuación, puede solicitar al usuario información adicional que necesita.  
  
 Las condiciones en las que el controlador solicita al usuario se controlan mediante la *DriverCompletion* marca; hay opciones para siempre le preguntará, símbolo del sistema si es necesario o nunca símbolo del sistema. Para obtener una descripción completa de esta marca, consulte la [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.

