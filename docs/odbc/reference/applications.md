---
title: Las aplicaciones | Documentos de Microsoft
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
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ba4e9a05f3dba74a973bf2b8b8a83a52ef78811
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="applications"></a>Aplicaciones
Un *aplicación* es un programa que llama a la API de ODBC para acceder a los datos. Aunque muchos tipos de aplicaciones son posibles, la mayoría se dividen en tres categorías, que se utilizan como ejemplos a lo largo de esta guía.  
  
-   **Aplicaciones genéricas** también se conocen como aplicaciones reducidas o aplicaciones comerciales. Aplicaciones genéricas están diseñadas para trabajar con una variedad de diferentes DBMS. Por ejemplo, una hoja de cálculo o un paquete de las estadísticas que utiliza ODBC para importar datos para su posterior análisis y un procesador de textos que utiliza ODBC para obtener una lista de distribución de correo desde una base de datos.  
  
     Una importante subcategoría de aplicaciones genéricas es entornos de desarrollo de aplicaciones, por ejemplo, PowerBuilder o Microsoft® Visual Basic®. Aunque las aplicaciones que se construyó con estos entornos probablemente solo funcionará con un DBMS único, el entorno en sí debe trabajar con varios DBMS.  
  
     Lo que todas las aplicaciones genéricas tienen en común es que son sumamente interoperativos entre DBMS y necesitan usar ODBC de forma relativamente genérica. Para obtener más información acerca de la interoperabilidad, consulte [elegir un nivel de interoperabilidad](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Las aplicaciones verticales** aplicaciones verticales realizar un solo tipo de tarea, como entrada de pedido o el seguimiento de datos de fabricación y trabajar con un esquema de base de datos que esté controlado por el desarrollador de la aplicación. Para un cliente concreto, la aplicación funciona con un DBMS único. Por ejemplo, una pequeña empresa puede usar la aplicación con dBase, mientras que una empresa de gran tamaño puede utilizar con Oracle.  
  
     La aplicación utiliza ODBC de tal forma que la aplicación no está asociada a cualquier un DBMS, aunque puede asociarse a un número limitado de DBMS que proporcionan una funcionalidad similar. Por lo tanto, el desarrollador de aplicaciones puede vender la aplicación sin que intervenga el DBMS. Las aplicaciones verticales son interoperables cuando se desarrollan pero a veces se han modificado para incluir código noninteroperable una vez que el cliente ha elegido un DBMS.  
  
-   **Aplicaciones personalizadas** aplicaciones personalizadas se utilizan para realizar una tarea específica en una única compañía. Por ejemplo, una aplicación en una gran compañía puede recopilar datos de ventas de varias divisiones (cada uno de los cuales usa un DBMS diferente) y crear un único informe. ODBC se utiliza porque es una interfaz común y evita que los programadores tengan que aprender varias interfaces. Estas aplicaciones no suelen ser interoperables y se escriben en DBMS y controladores específicos.  
  
 Una serie de tareas es comunes a todas las aplicaciones, con independencia de cómo usan ODBC. Tomadas juntas, en gran medida definen el flujo de cualquier aplicación de ODBC. Las tareas son:  
  
-   Seleccionar un origen de datos y conectarse a él.  
  
-   Enviar una instrucción SQL para la ejecución.  
  
-   Al recuperar los resultados (si existe).  
  
-   Errores de procesamiento.  
  
-   Confirmar o revertir la transacción incluye la instrucción SQL.  
  
-   Desconectando el origen de datos.  
  
 Dado que se hace la mayor parte del trabajo acceso a datos con SQL, es la tarea principal para que las aplicaciones utilizan ODBC enviar instrucciones SQL y recuperar los resultados (si existe) generados por esas instrucciones. Otras tareas para que las aplicaciones utilizan ODBC incluyen determinar y ajustar a las capacidades de controlador y examinar el catálogo de base de datos.
