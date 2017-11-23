---
title: "Usos de los datos del catálogo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c77be1b431a7f7e2cf8c040df7ceb9a9feaf321a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="uses-of-catalog-data"></a>Usos de los datos del catálogo
Aplicaciones utilizan datos de catálogo en una variedad de formas. Estos son algunos usos habituales:  
  
-   **Crear instrucciones SQL en tiempo de ejecución.** Las aplicaciones verticales, como una aplicación de entrada de pedidos, contienen instrucciones de SQL codificadas de forma rígida. Las tablas y columnas que se usan por la aplicación se fijan antes de tiempo, como son las instrucciones que tienen acceso a estas tablas. Por ejemplo, una aplicación de entrada de pedidos contiene normalmente una única con parámetros **insertar** instrucción para agregar nuevos pedidos en el sistema.  
  
     Aplicaciones genéricas, por ejemplo, un programa de hoja de cálculo que utiliza ODBC para recuperar datos, a menudo construcción instrucciones SQL en tiempo de ejecución basándose en la entrada del usuario. Este tipo de aplicación podría solicitar al usuario que escriba los nombres de las tablas y columnas que desea usar. Sin embargo, sería más fácil para el usuario si la aplicación muestra listas de tablas y columnas desde el que el usuario puede realizar selecciones. Para compilar estas listas, se llamaría la aplicación la **SQLTables** y **SQLColumns** las funciones de catálogo.  
  
-   **Crear instrucciones SQL durante el desarrollo.** Normalmente, los entornos de desarrollo de aplicaciones permiten al programador crear consultas de base de datos durante el desarrollo de un programa. Las consultas, a continuación, están codificados en la aplicación que se está genera.  
  
     También pudieron usar dichos entornos **SQLTables** y **SQLColumns** para crear listas desde la que el programador puede realizar selecciones. También pueden usar estos entornos **SQLPrimaryKeys** y **SQLForeignKeys** para determinar y mostrar las relaciones entre las tablas seleccionadas y usar automáticamente **SQLStatistics** para determinar y resaltar los campos indizados por lo que el programador puede crear consultas eficaces.  
  
-   **La construcción de los cursores.** Podría usar una aplicación, controlador o software intermedio que proporciona un motor de cursor desplazable **SQLSpecialColumns** para determinar qué columna o columnas identifican una fila. El programa podría generar un *keyset* que contiene los valores de estas columnas para cada fila que se han capturado. Cuando la aplicación se desplaza a la fila, utilizaría, a continuación, estos valores para capturar los datos más recientes de la fila. Para obtener más información acerca de los cursores desplazables y conjuntos de claves, consulte [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).
