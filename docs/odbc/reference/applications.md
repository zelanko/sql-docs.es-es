---
title: Las aplicaciones | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc655740701822d8c6ff9595327b906ee9a67026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735001"
---
# <a name="applications"></a>Aplicaciones
Un *aplicación* es un programa que llama a la API de ODBC para acceder a los datos. Aunque son posibles muchos tipos de aplicaciones, la mayoría se dividen en tres categorías, que se utilizan como ejemplos en esta guía.  
  
-   **Aplicaciones genéricas** también se conocen como aplicaciones empaquetadas o las aplicaciones estandarizadas. Aplicaciones genéricas están diseñadas para funcionar con una variedad de diferentes DBMS. Por ejemplo, una hoja de cálculo o paquete de estadísticas que utiliza ODBC para importar datos para su posterior análisis y un procesador de textos que usa ODBC para obtener una lista de distribución de correo electrónico desde una base de datos.  
  
     Una importante subcategoría de aplicaciones genéricas es entornos de desarrollo de aplicaciones, como PowerBuilder o Microsoft® Visual Basic®. Aunque las aplicaciones que se construye con estos entornos es probable que funcione solo con un DBMS único, el propio entorno debe trabajar con varios DBMS.  
  
     Lo que todas las aplicaciones genéricas tienen en común es que son muy interoperables entre DBMS y que necesitan usar ODBC en una manera relativamente genérica. Para obtener más información acerca de la interoperabilidad, consulte [elegir un nivel de interoperabilidad](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicaciones verticales** aplicaciones verticales realizar un único tipo de tarea, como la entrada de orden o seguimiento de los datos de fabricación y trabajar con un esquema de base de datos que esté controlado por el desarrollador de la aplicación. Para un cliente concreto, la aplicación funciona con un DBMS único. Por ejemplo, una pequeña empresa puede usar la aplicación con dBase, mientras que una gran empresa puede utilizar con Oracle.  
  
     La aplicación utiliza ODBC de tal manera que la aplicación no está asociada a cualquier un DBMS, aunque lo se puede vincular a un número limitado de DBMS que proporcionan una funcionalidad similar. Por lo tanto, el desarrollador de aplicaciones puede vender la aplicación independientemente de la instancia de DBMS. Aplicaciones verticales son interoperables cuando se desarrollan pero a veces se han modificado para incluir código noninteroperable una vez que el cliente ha elegido un DBMS.  
  
-   **Aplicaciones personalizadas** las aplicaciones personalizadas se usan para realizar una tarea específica en una empresa. Por ejemplo, una aplicación en una gran empresa podría recopilar datos de ventas de varias divisiones (cada uno de los cuales usa un DBMS diferente) y crear un informe único. Se utiliza ODBC porque es una interfaz común y evita que los programadores de tener que aprender varias interfaces. Estas aplicaciones no suelen ser interoperables y se escriben en los controladores y los DBMS específicos.  
  
 Un número de tareas es comunes a todas las aplicaciones, independientemente de cómo usan ODBC. En conjunto, definen el flujo de cualquier aplicación ODBC en gran medida. Las tareas son:  
  
-   Al seleccionar un origen de datos y se conecta a él.  
  
-   Enviar una instrucción SQL para su ejecución.  
  
-   Al recuperar los resultados (si existe).  
  
-   Errores de procesamiento.  
  
-   Confirmar o revertir la transacción en la envolvente de la instrucción SQL.  
  
-   Desconectar del origen de datos.  
  
 Dado que la mayoría del trabajo acceso a datos se realiza con SQL, es la tarea principal para que las aplicaciones utilizar ODBC enviar instrucciones SQL y recuperar los resultados generados por esas instrucciones (si existe). Otras tareas para que las aplicaciones utilizar ODBC incluyen determinar y ajustar a las capacidades del controlador y exploración del catálogo de base de datos.
