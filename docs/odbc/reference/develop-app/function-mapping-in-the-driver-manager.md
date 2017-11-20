---
title: "Función de asignación en el Administrador de controladores | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4ea01836108b8cf2524aa52001927bef852ce2a1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="function-mapping-in-the-driver-manager"></a>Asignación de función en el Administrador de controladores
El Administrador de controladores es compatible con dos puntos de entrada para las funciones que toman argumentos de cadena. La función no representativa (**SQLDriverConnect**) es la forma ANSI de la función. La forma de Unicode se decora con un *W* (**SQLDriverConnectW**.)  
  
 El archivo de encabezado ODBC también admite funciones decoradas con un *A* (**SQLDriverConnectA**) para la comodidad de aplicaciones mixtas de ANSI o Unicode. Las llamadas realizadas a la **A** funciones son en realidad llama en el punto de entrada no representativo (**SQLDriverConnect**.)  
  
 Si la aplicación se compila con la _UNICODE **#define**, el archivo de encabezado ODBC asignará las llamadas a funciones no representativo (**SQLDriverConnect**) a la versión de Unicode (**SQLDriverConnectW** .)  
  
 El Administrador de controladores reconoce un controlador como un controlador de Unicode si **SQLConnectW** es compatible con el controlador.  
  
 Si el controlador es un controlador de Unicode, el Administrador de controladores realiza llamadas a función como sigue:  
  
-   Pasa una función sin argumentos de cadena o los parámetros directamente a través del controlador.  
  
-   Pasa las funciones Unicode (con la *W* sufijo) directamente desde el controlador.  
  
-   Convierte una función de ANSI (con la *A* sufijo) a una función de Unicode (con la *W* sufijo) mediante la conversión de los argumentos de cadena en Unicode caracteres y devuelve la función Unicode al controlador.  
  
 Si el controlador es un controlador de ANSI, el Administrador de controladores realiza llamadas a función como sigue:  
  
-   Funciones sin argumentos de cadena o los parámetros directamente a través de se pasa al controlador.  
  
-   Convierte las funciones Unicode (con la *W* sufijo) llamada de función a un ANSI y lo pasa al controlador.  
  
-   Devuelve una función ANSI directamente al controlador.  
  
 El Administrador de controladores está habilitada para Unicode internamente. Como resultado, el rendimiento óptimo se obtiene con una aplicación Unicode que se trabaja con un controlador de Unicode, debido a que el Administrador de controladores simplemente pasa las funciones de Unicode a través del controlador. Cuando una aplicación ANSI está trabajando con un controlador de ANSI, el Administrador de controladores debe convertir las cadenas de ANSI a Unicode al procesamiento de algunas funciones, como **SQLDriverConnect**. Después de procesar la función, el Administrador de controladores, a continuación, debe convertir la cadena de Unicode a ANSI antes de enviar la función del controlador de ANSI.  
  
 Una aplicación no debe modificar ni leer sus búferes de parámetros enlazados cuando el controlador devuelve SQL_NEED_DATA o SQL_STILL_EXECUTING. El Administrador de controladores deja los búferes que se enlazan a ANSI hasta que el controlador devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Una aplicación multiproceso no debe obtener acceso a los valores de parámetros enlazados que otro subproceso se está ejecutando una instrucción SQL. El Administrador de controladores convierte los datos de Unicode a ANSI "en contexto" y el otro subproceso se vean datos ANSI en estos búferes mientras el controlador todavía está procesando la instrucción SQL. Las aplicaciones que se enlazan datos Unicode a un controlador de ANSI no deben enlazar dos columnas diferentes a la misma dirección.

