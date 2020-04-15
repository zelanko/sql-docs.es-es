---
title: Opciones de la declaración ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299215"
---
# <a name="statement-options"></a>Opciones de la instrucción
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Estas opciones permiten la personalización de una instrucción de ejecución específica dentro de una aplicación.  
  
|Opción de declaración|Notas|  
|----------------------|-----------|  
|SQL_BIND_TYPE|No se pueden superar los 2.147.483.647 bytes ni la memoria disponible.|  
|SQL_CONCURRENCY|Para conocer los valores [permitidos,](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)vea Combinaciones de tipo de cursor y simultaneidad .|  
|SQL_CURSOR_TYPE|El controlador no permite SQL_CURSOR_DYNAMIC. Consulte [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) para obtener más información. Para conocer los valores [permitidos,](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)vea Combinaciones de tipo de cursor y simultaneidad .|  
|SQL_GET_BOOKMARK|Devuelve un valor entero de 32 bits que es el marcador para el número de registro actual. Obtener sólo; no se puede establecer.|  
|SQL_KEYSET_SIZE|Solo se puede establecer en 0.|  
|SQL_MAX_ROWS|El número máximo de filas que se devolverán de un conjunto de resultados.|  
|SQL_ROW_NUMBER|Devuelve un entero de 32 bits que especifica la posición de la fila actual dentro del conjunto de resultados. Obtener sólo; no se puede establecer.|  
|SQL_ROWSET_SIZE|No se pueden superar las 4.294.967.296 filas; sin embargo, debe tener suficiente memoria virtual en el equipo para gestionar su solicitud.|  
|SQL_USE_BOOKMARKS|Admite la configuración de SQL_USE_BOOKMARKS en SQL_UB_ON y expone marcadores de longitud fija.|
