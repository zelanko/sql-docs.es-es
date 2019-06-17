---
title: En el Administrador de controladores de asignación de función | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- driver manager [ODBC], function mapping
- functions [ODBC], Unicode functions
ms.assetid: ff093b29-671a-4fc0-86c9-08a311a98e54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40dc214fa7f77dfb81c941095ecd71d3d4bf5a36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061563"
---
# <a name="function-mapping-in-the-driver-manager"></a>Asignación de función en el Administrador de controladores
El Administrador de controladores es compatible con dos puntos de entrada para las funciones que toman argumentos de cadena. La función no representativa (**SQLDriverConnect**) es la forma ANSI de la función. La forma de Unicode está decorada con un *W* (**SQLDriverConnectW**.)  
  
 El archivo de encabezado ODBC también admite funciones decoradas con un *A,* (**SQLDriverConnectA**) para facilitar el trabajo de aplicaciones combinadas de ANSI o Unicode. Las llamadas realizadas a la **A** funciones son en realidad llama en el punto de entrada no representativo (**SQLDriverConnect**.)  
  
 Si la aplicación se compila con la _UNICODE **#define**, el archivo de encabezado ODBC asignará las llamadas de función no representativos (**SQLDriverConnect**) a la versión de Unicode (**SQLDriverConnectW** .)  
  
 El Administrador de controladores reconoce un controlador como un controlador de Unicode si **SQLConnectW** es compatible con el controlador.  
  
 Si el controlador es un controlador de Unicode, el Administrador de controladores realiza llamadas a función como sigue:  
  
-   Pasa una función sin argumentos de cadena o los parámetros directamente a través del controlador.  
  
-   Pasa las funciones Unicode (con el *W* sufijo) directamente a través del controlador.  
  
-   Convierte una función ANSI (con el *A* sufijo) a una función de Unicode (con el *W* sufijo) al convertir los argumentos de cadena en Unicode caracteres y pasa la función Unicode para el controlador.  
  
 Si el controlador es un controlador de ANSI, el Administrador de controladores realiza llamadas a función como sigue:  
  
-   Funciones sin argumentos de cadena o los parámetros directamente a través se pasa al controlador.  
  
-   Convierte las funciones Unicode (con el *W* sufijo) llamada de función a un ANSI y lo pasa al controlador.  
  
-   Una función ANSI se pasa directamente al controlador.  
  
 El Administrador de controladores está habilitada para Unicode internamente. Como resultado, se obtiene un rendimiento óptimo por una aplicación Unicode trabaja con un controlador de Unicode, porque el Administrador de controladores simplemente pasa a través de las funciones de Unicode al controlador. Cuando una aplicación ANSI está trabajando con un controlador de ANSI, el Administrador de controladores debe convertir las cadenas de ANSI a Unicode al procesamiento de algunas funciones, como **SQLDriverConnect**. Después de procesar la función, el Administrador de controladores, a continuación, debe convertir la cadena de Unicode a ANSI antes de enviar la función para el controlador de ANSI.  
  
 Una aplicación no debe modificar o leer sus búferes de parámetros enlazados, cuando el controlador devuelve SQL_NEED_DATA o SQL_STILL_EXECUTING. El Administrador de controladores deja los búferes enlazados a ANSI hasta que el controlador devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Una aplicación multiproceso no debe tener acceso a los valores de parámetros enlazados que otro subproceso ejecuta una instrucción SQL en. El Administrador de controladores convierte los datos de Unicode a ANSI "en contexto" y el otro subproceso podría ver datos ANSI en estos búferes mientras el controlador todavía está procesando la instrucción SQL. Las aplicaciones que se enlazan datos Unicode con un controlador de ANSI no deben enlazar dos columnas diferentes a la misma dirección.
