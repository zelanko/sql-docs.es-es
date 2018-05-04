---
title: Opciones de la instrucción | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75a4eef546e37fea71e88fa5d8926c7b5bd95ac2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="statement-options"></a>Opciones de la instrucción
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Estas opciones permiten la personalización de una instrucción de ejecución concreta dentro de una aplicación.  
  
|Opción de instrucción|Notas|  
|----------------------|-----------|  
|SQL_BIND_TYPE|No puede superar 2.147.483.647 bytes o la memoria disponible.|  
|SQL_CONCURRENCY|Para los valores permitidos, consulte la [combinaciones de simultaneidad y el tipo de Cursor](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|El controlador no permite SQL_CURSOR_DYNAMIC. Vea [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) para obtener más información. Para los valores permitidos, consulte la [combinaciones de simultaneidad y el tipo de Cursor](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Devuelve un valor entero de 32 bits que es el marcador para el número de registro actual. Obtener solo; no se puede establecer.|  
|SQL_KEYSET_SIZE|Puede establecerse únicamente en 0.|  
|SQL_MAX_ROWS|Establece el número máximo de filas que se va a devolver de un resultado.|  
|SQL_ROW_NUMBER|Devuelve un entero de 32 bits que especifica la posición de la fila actual en el conjunto de resultados. Obtener solo; no se puede establecer.|  
|SQL_ROWSET_SIZE|No puede superar los 4.294.967.296 filas; Sin embargo, debe tener suficiente memoria virtual en el equipo para atender la solicitud.|  
|SQL_USE_BOOKMARKS|Admite el establecimiento de SQL_USE_BOOKMARKS a SQL_UB_ON y expone marcadores de longitud fija.|
