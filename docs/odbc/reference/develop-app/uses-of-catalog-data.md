---
title: Usos de los datos del catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc8999c0a7189772145f553646b45eb1f1fbd695
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091614"
---
# <a name="uses-of-catalog-data"></a>Usos de los datos del catálogo
Las aplicaciones usan datos de catálogo de varias maneras. Estos son algunos usos comunes:  
  
-   **Construir instrucciones SQL en tiempo de ejecución.** Las aplicaciones verticales, como una aplicación de entrada de pedidos, contienen instrucciones SQL codificadas de forma rígida. Las tablas y columnas que usa la aplicación se fijan con anterioridad, al igual que las instrucciones que tienen acceso a estas tablas. Por ejemplo, una aplicación de entrada de pedidos normalmente contiene una única instrucción **Insert** con parámetros para agregar nuevos pedidos al sistema.  
  
     Las aplicaciones genéricas, como un programa de hoja de cálculo que usa ODBC para recuperar datos, suelen construir instrucciones SQL en tiempo de ejecución en función de la entrada del usuario. Este tipo de aplicación podría requerir que el usuario escriba los nombres de las tablas y columnas que se van a utilizar. Sin embargo, sería más sencillo para el usuario si la aplicación mostrara listas de tablas y columnas desde las que el usuario podía realizar selecciones. Para compilar estas listas, la aplicación llamaría a las funciones de catálogo **SQLTables** y **SQLColumns** .  
  
-   **Construir instrucciones SQL durante el desarrollo.** Los entornos de desarrollo de aplicaciones suelen permitir al programador crear consultas de base de datos al desarrollar un programa. Las consultas se codifican de forma rígida en la aplicación que se está compilando.  
  
     Estos entornos también podrían usar **SQLTables** y **SQLColumns** para crear listas desde las que el programador podría hacer selecciones. Estos entornos también pueden usar **SQLPrimaryKeys** y **SQLForeignKeys** para determinar y mostrar automáticamente las relaciones entre las tablas seleccionadas, y usar **SQLStatistics** para determinar y resaltar los campos indexados para que el programador pueda crear consultas eficaces.  
  
-   **Construir cursores.** Una aplicación, un controlador o un middleware que proporciona un motor de cursor desplazable podría usar **SQLSpecialColumns** para determinar qué columna o columnas identifican de forma única una fila. El programa podría generar un *conjunto de claves* que contenga los valores de estas columnas para cada fila que se ha capturado. Cuando la aplicación se desplaza de nuevo a la fila, utilizará estos valores para obtener los datos más recientes de la fila. Para obtener más información sobre los cursores desplazables y conjuntos, vea [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).
