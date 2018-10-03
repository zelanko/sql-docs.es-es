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
manager: craigg
ms.openlocfilehash: d9b75d59d8fc28e364f5826d95e7fc50cb6afda7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622313"
---
# <a name="uses-of-catalog-data"></a>Usos de los datos del catálogo
Las aplicaciones utilizar los datos del catálogo en una variedad de formas. Estos son algunos usos habituales:  
  
-   **Crear instrucciones SQL en tiempo de ejecución.** Aplicaciones verticales, como una aplicación de entrada de pedidos, contienen las instrucciones SQL codificadas de forma rígida. Las tablas y columnas que se usan por la aplicación son fijos antes de tiempo, como son las instrucciones que tienen acceso a estas tablas. Por ejemplo, una aplicación de entrada de pedidos normalmente contiene un único, con parámetros **insertar** instrucción para agregar nuevos pedidos para el sistema.  
  
     Aplicaciones genéricas, por ejemplo, un programa de hoja de cálculo que usa ODBC para recuperar datos, a menudo construcción instrucciones SQL en tiempo de ejecución basándose en la entrada del usuario. Este tipo de aplicación podría requerir al usuario que escriba los nombres de las tablas y columnas que desea usar. Sin embargo, sería más fácil para el usuario si la aplicación muestra las listas de tablas y columnas desde el que el usuario podría realizar selecciones. Para crear estas listas, se llamaría la aplicación la **SQLTables** y **SQLColumns** funciones de catálogo.  
  
-   **Crear instrucciones SQL durante el desarrollo.** Entornos de desarrollo de aplicaciones normalmente permiten al programador crear consultas de base de datos al desarrollar un programa. Las consultas, a continuación, están codificados en la aplicación que se está compila.  
  
     También podrían usar dichos entornos **SQLTables** y **SQLColumns** para crear listas desde el que el programador puede realizar selecciones. También pueden usar estos entornos **SQLPrimaryKeys** y **SQLForeignKeys** para determinar y mostrar las relaciones entre tablas seleccionadas y usar automáticamente **SQLStatistics** para determinar y resaltar los campos indizados por lo que el programador puede crear consultas eficaces.  
  
-   **Creación de los cursores.** Podría usar una aplicación, controlador o software intermedio que proporciona un motor de cursor desplazable **SQLSpecialColumns** para determinar qué columna o columnas identifican inequívocamente una fila. El programa podría generar un *keyset* que contiene los valores de estas columnas para cada fila que se han obtenido. Cuando la aplicación se desplaza a la fila, a continuación, utilizaría estos valores para capturar los datos más recientes para la fila. Para obtener más información acerca de los cursores desplazables y conjuntos de claves, consulte [los cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md).
