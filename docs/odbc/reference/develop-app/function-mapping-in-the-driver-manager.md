---
title: Asignación de funciones en el Administrador de controladores ( Driver Manager) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db8e525bb7e8f3e167deb8061a4dd5b75073933c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305586"
---
# <a name="function-mapping-in-the-driver-manager"></a>Asignación de función en el Administrador de controladores
El administrador de controladores admite dos puntos de entrada para las funciones que toman argumentos de cadena. La función no decorada (**SQLDriverConnect**) es la forma ANSI de la función. El formulario Unicode está decorado con un *W* (**SQLDriverConnectW**.)  
  
 El archivo de encabezado ODBC también admite funciones decoradas con un *A,* (**SQLDriverConnectA**) para la comodidad de aplicaciones ANSI/Unicode mixtas. Las llamadas realizadas a las funciones **A** son en realidad llamadas al punto de entrada no decorado (**SQLDriverConnect**.)  
  
 Si la aplicación se compila con el **_UNICODE #define**, el archivo de encabezado ODBC asignará llamadas de función no decoradas (**SQLDriverConnect**) a la versión Unicode (**SQLDriverConnectW**.)  
  
 El Administrador de controladores reconoce un controlador como un controlador Unicode si **SQLConnectW** es compatible con el controlador.  
  
 Si el controlador es un controlador Unicode, el Administrador de controladores realiza llamadas de función de la siguiente manera:  
  
-   Pasa una función sin argumentos de cadena o parámetros directamente al controlador.  
  
-   Pasa las funciones Unicode (con el sufijo *W)* directamente al controlador.  
  
-   Convierte una función ANSI (con el sufijo *A)* en una función Unicode (con el sufijo *W)* convirtiendo los argumentos de cadena en caracteres Unicode y pasa la función Unicode al controlador.  
  
 Si el controlador es un controlador ANSI, el Administrador de controladores realiza llamadas de función de la siguiente manera:  
  
-   Pasa funciones sin argumentos de cadena o parámetros directamente al controlador.  
  
-   Convierte funciones Unicode (con el sufijo *W)* en una llamada de función ANSI y la pasa al controlador.  
  
-   Pasa una función ANSI directamente al controlador.  
  
 El Administrador de controladores está habilitado para Unicode internamente. Como resultado, el rendimiento óptimo se obtiene mediante una aplicación Unicode que trabaja con un controlador Unicode, ya que el Administrador de controladores simplemente pasa las funciones Unicode al controlador. Cuando una aplicación ANSI está trabajando con un controlador ANSI, el Administrador de controladores debe convertir cadenas de ANSI a Unicode al procesar algunas funciones, como **SQLDriverConnect**. Después de procesar la función, el Administrador de controladores debe convertir la cadena Unicode a ANSI antes de enviar la función al controlador ANSI.  
  
 Una aplicación no debe modificar ni leer sus búferes de parámetros enlazados cuando el controlador devuelve SQL_STILL_EXECUTING o SQL_NEED_DATA. El Administrador de controladores deja los búferes enlazados a ANSI hasta que el controlador devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO o SQL_ERROR. Una aplicación multiproceso no debe obtener acceso a los valores de parámetro enlazados en los que otro subproceso está ejecutando una instrucción SQL. El Administrador de controladores convierte los datos de Unicode a ANSI "en su lugar", y el otro subproceso puede ver datos ANSI en estos búferes mientras el controlador todavía está procesando la instrucción SQL. Las aplicaciones que enlazan datos Unicode a un controlador ANSI no deben enlazar dos columnas diferentes a la misma dirección.
