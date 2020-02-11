---
title: Opciones de instrucción | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bf99aace8b058e429898846466294cc42612070
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948834"
---
# <a name="statement-options"></a>Opciones de la instrucción
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Estas opciones permiten la personalización de una instrucción de ejecución específica dentro de una aplicación.  
  
|Opción de instrucción|Notas|  
|----------------------|-----------|  
|SQL_BIND_TYPE|No puede superar 2.147.483.647 bytes o memoria disponible.|  
|SQL_CONCURRENCY|Para los valores permitidos, vea el [tipo de cursor y las combinaciones de simultaneidad](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|El controlador no permite SQL_CURSOR_DYNAMIC. Vea [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) para obtener más información. Para los valores permitidos, vea el [tipo de cursor y las combinaciones de simultaneidad](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Devuelve un valor entero de 32 bits que es el marcador para el número de registro actual. Solo obtener; no se puede establecer.|  
|SQL_KEYSET_SIZE|Solo se puede establecer en 0.|  
|SQL_MAX_ROWS|Número máximo de filas que se van a devolver de un conjunto de resultados.|  
|SQL_ROW_NUMBER|Devuelve un entero de 32 bits que especifica la posición de la fila actual dentro del conjunto de resultados. Solo obtener; no se puede establecer.|  
|SQL_ROWSET_SIZE|No puede superar 4.294.967.296 filas; sin embargo, debe tener suficiente memoria virtual en el equipo para controlar la solicitud.|  
|SQL_USE_BOOKMARKS|Permite establecer SQL_USE_BOOKMARKS en SQL_UB_ON y expone marcadores de longitud fija.|
