---
title: Aplicaciones ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9184986883f64bd082ca1db472d887609d3071bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306556"
---
# <a name="applications"></a>APLICACIONES
Una *aplicación* es un programa que llama a la API ODBC para tener acceso a los datos. Aunque muchos tipos de aplicaciones son posibles, la mayoría se dividen en tres categorías, que se utilizan como ejemplos a lo largo de esta guía.  
  
-   **Aplicaciones genéricas** También se conocen como aplicaciones envueltas en contracción o aplicaciones listas para usar. Las aplicaciones genéricas están diseñadas para trabajar con una variedad de DBMS diferentes. Los ejemplos incluyen una hoja de cálculo o un paquete de estadísticas que usa ODBC para importar datos para su análisis posterior y un procesador de textos que usa ODBC para obtener una lista de correo de una base de datos.  
  
     Una subcategoría importante de aplicaciones genéricas son los entornos de desarrollo de aplicaciones, como PowerBuilder o Microsoft® Visual Basic®. Aunque las aplicaciones construidas con estos entornos probablemente solo funcionarán con un único DBMS, el propio entorno necesita trabajar con varios DBMS.  
  
     Lo que todas las aplicaciones genéricas tienen en común es que son altamente interoperables entre los DBMS y necesitan usar ODBC de una manera relativamente genérica. Para obtener más información acerca de la interoperabilidad, consulte [Elegir un nivel de interoperabilidad](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicaciones verticales** Las aplicaciones verticales realizan un único tipo de tarea, como la entrada de pedidos o el seguimiento de datos de fabricación, y funcionan con un esquema de base de datos controlado por el desarrollador de la aplicación. Para un cliente determinado, la aplicación funciona con un único DBMS. Por ejemplo, una pequeña empresa podría utilizar la aplicación con dBase, mientras que una gran empresa podría usarla con Oracle.  
  
     La aplicación utiliza ODBC de tal manera que la aplicación no está vinculada a ningún DBMS, aunque podría estar vinculada a un número limitado de DBMS que proporcionan una funcionalidad similar. Por lo tanto, el desarrollador de aplicaciones puede vender la aplicación independientemente del DBMS. Las aplicaciones verticales son interoperables cuando se desarrollan, pero a veces se modifican para incluir código no interoperable una vez que el cliente ha elegido un DBMS.  
  
-   **Aplicaciones personalizadas** Las aplicaciones personalizadas se utilizan para realizar una tarea específica en una sola empresa. Por ejemplo, una aplicación de una empresa grande podría recopilar datos de ventas de varias divisiones (cada una de las cuales utiliza un DBMS diferente) y crear un único informe. ODBC se utiliza porque es una interfaz común y evita que los programadores tengan que aprender varias interfaces. Estas aplicaciones generalmente no son interoperables y se escriben en DBMS y controladores específicos.  
  
 Una serie de tareas son comunes a todas las aplicaciones, independientemente de cómo usen ODBC. En conjunto, definen en gran medida el flujo de cualquier aplicación ODBC. Las tareas son:  
  
-   Seleccionar un origen de datos y conectarse a él.  
  
-   Envío de una instrucción SQL para su ejecución.  
  
-   Recuperación de resultados (si los hay).  
  
-   Errores de procesamiento.  
  
-   Confirmar o revertir la transacción que encierra la instrucción SQL.  
  
-   Desconectarse del origen de datos.  
  
 Dado que la mayoría del trabajo de acceso a datos se realiza con SQL, la tarea principal para la que las aplicaciones usan ODBC es enviar instrucciones SQL y recuperar los resultados (si los hay) generados por esas instrucciones. Otras tareas para las que las aplicaciones usan ODBC incluyen determinar y ajustar a las capacidades del controlador y examinar el catálogo de bases de datos.
