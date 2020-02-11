---
title: Asignación de función en el administrador de controladores | Microsoft Docs
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
ms.openlocfilehash: 2bfa535d4175c109e96098dd1e40e93be9521de2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069689"
---
# <a name="function-mapping-in-the-driver-manager"></a>Asignación de función en el Administrador de controladores
El administrador de controladores admite dos puntos de entrada para las funciones que toman argumentos de cadena. La función no representativa (**SQLDriverConnect**) es la forma ANSI de la función. El formato Unicode se decora con un *W* (**SQLDriverConnectW**).  
  
 El archivo de encabezado ODBC también admite funciones decoradas con un *,* (**SQLDriverConnectA**) para la comodidad de las aplicaciones ANSI/Unicode mixtas. Las llamadas realizadas a las funciones **de** son en realidad llamadas en el punto de entrada no representativo (**SQLDriverConnect**).  
  
 Si la aplicación se compila con el **#define**_UNICODE, el archivo de encabezado ODBC asignará las llamadas de función no representativas (**SQLDriverConnect**) a la versión Unicode (**SQLDriverConnectW**).  
  
 El administrador de controladores reconoce un controlador como un controlador Unicode si el controlador es compatible con **SQLConnectW** .  
  
 Si el controlador es un controlador Unicode, el administrador de controladores realiza las llamadas de función de la manera siguiente:  
  
-   Pasa una función sin argumentos de cadena ni parámetros directamente a través del controlador.  
  
-   Pasa directamente las funciones Unicode (con el sufijo *W* ) al controlador.  
  
-   Convierte una función ANSI (con el sufijo) en una función Unicode ( *con el sufijo* *W* ) convirtiendo los argumentos de cadena en caracteres Unicode y pasa la función Unicode al controlador.  
  
 Si el controlador es un controlador ANSI, el administrador de controladores realiza las llamadas de función de la manera siguiente:  
  
-   Pasa funciones sin argumentos de cadena ni parámetros directamente a través del controlador.  
  
-   Convierte las funciones Unicode (con el sufijo *W* ) en una llamada de función ANSI y la pasa al controlador.  
  
-   Pasa una función ANSI directamente al controlador.  
  
 El administrador de controladores está habilitado para Unicode internamente. Como resultado, una aplicación Unicode que trabaja con un controlador Unicode obtiene el rendimiento óptimo, ya que el administrador de controladores simplemente pasa las funciones Unicode a través del controlador. Cuando una aplicación ANSI trabaja con un controlador ANSI, el administrador de controladores debe convertir las cadenas de ANSI a Unicode al procesar algunas funciones, como **SQLDriverConnect**. Después de procesar la función, el administrador de controladores debe volver a convertir la cadena Unicode en ANSI antes de enviar la función al controlador ANSI.  
  
 Una aplicación no debe modificar ni leer sus búferes de parámetros enlazados cuando el controlador devuelve SQL_STILL_EXECUTING o SQL_NEED_DATA. El administrador de controladores deja los búferes enlazados a ANSI hasta que el controlador devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Una aplicación multiproceso no debe obtener acceso a los valores de parámetro enlazados en los que otro subproceso está ejecutando una instrucción SQL. El administrador de controladores convierte los datos de Unicode a ANSI "in situ" y el otro subproceso podría ver datos ANSI en estos búferes mientras el controlador sigue procesando la instrucción SQL. Las aplicaciones que enlazan datos Unicode a un controlador ANSI no deben enlazar dos columnas diferentes a la misma dirección.
