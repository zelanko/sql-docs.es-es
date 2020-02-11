---
title: Aplicaciones | Microsoft Docs
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
ms.openlocfilehash: f15b5e8eb6eb7c63ab771030f0c31e8c9ff92724
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135682"
---
# <a name="applications"></a>APLICACIONES
Una *aplicación* es un programa que llama a la API de ODBC para obtener acceso a los datos. Aunque muchos tipos de aplicaciones son posibles, la mayoría de ellas se dividen en tres categorías, que se usan como ejemplos a lo largo de esta guía.  
  
-   **Aplicaciones genéricas** También se conocen como aplicaciones ajustadas para la reducción o aplicaciones de uso no controlado. Las aplicaciones genéricas están diseñadas para trabajar con distintos DBMS. Entre los ejemplos se incluye una hoja de cálculo o un paquete de estadísticas que usa ODBC para importar datos para su posterior análisis y un procesador de textos que usa ODBC para obtener una lista de distribución de correo de una base de datos.  
  
     Una subcategoría importante de las aplicaciones genéricas son los entornos de desarrollo de aplicaciones, como PowerBuilder o Microsoft® Visual Basic®. Aunque es probable que las aplicaciones construidas con estos entornos solo funcionen con un único DBMS, el propio entorno debe trabajar con varios DBMS.  
  
     Lo que tienen todas las aplicaciones genéricas en común es que son altamente interoperables entre DBMS y necesitan usar ODBC de una manera relativamente genérica. Para obtener más información sobre la interoperabilidad, vea [elegir un nivel de interoperabilidad](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicaciones verticales** Las aplicaciones verticales realizan un único tipo de tarea, como la entrada de pedidos o el seguimiento de los datos de fabricación, y el trabajo con un esquema de base de datos controlado por el desarrollador de la aplicación. Para un cliente determinado, la aplicación funciona con un solo DBMS. Por ejemplo, una pequeña empresa podría usar la aplicación con dBase, mientras que una empresa grande podría usarla con Oracle.  
  
     La aplicación utiliza ODBC de modo que la aplicación no está asociada a ningún DBMS, aunque podría estar vinculada a un número limitado de DBMS que proporcionan una funcionalidad similar. Por lo tanto, el desarrollador de la aplicación puede vender la aplicación independientemente del DBMS. Las aplicaciones verticales son interoperables cuando se desarrollan, pero a veces se modifican para incluir código de noninteroperable una vez que el cliente ha elegido un DBMS.  
  
-   **Aplicaciones personalizadas** Las aplicaciones personalizadas se usan para realizar una tarea específica en una sola empresa. Por ejemplo, una aplicación de una gran empresa puede recopilar datos de ventas de varias divisiones (cada una de las cuales usa un DBMS diferente) y crear un único informe. Se usa ODBC porque es una interfaz común y evita que los programadores tengan que aprender varias interfaces. Por lo general, estas aplicaciones no son interoperables y se escriben en DBMS y controladores específicos.  
  
 Algunas tareas son comunes a todas las aplicaciones, independientemente de cómo utilicen ODBC. En conjunto, definen en gran medida el flujo de cualquier aplicación ODBC. Las tareas son las siguientes:  
  
-   Seleccionar un origen de datos y conectarse a él.  
  
-   Enviar una instrucción SQL para su ejecución.  
  
-   Recuperando resultados (si existen).  
  
-   Errores de procesamiento.  
  
-   Confirmar o revertir la transacción que contiene la instrucción SQL.  
  
-   Desconectarse del origen de datos.  
  
 Dado que la mayor parte del trabajo de acceso a los datos se realiza con SQL, la tarea principal para la que las aplicaciones utilizan ODBC es enviar instrucciones SQL y recuperar los resultados (si existen) generados por esas instrucciones. Otras tareas para las que las aplicaciones utilizan ODBC son determinar y ajustar a las capacidades del controlador y examinar el catálogo de la base de datos.
