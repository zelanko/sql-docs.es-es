---
title: Datos de la columna | Documentos de Microsoft
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
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7694a2646f8cb62824991d37a01cd49f5291033
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="column-data"></a>Datos de columna
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para los búferes de datos enlazados en el conjunto de resultados con **SQLBindCol**. Usa los valores en estos búferes para construir un **donde** cláusula cuando emula una posición instrucción update o delete. Actualiza estos búferes de los búferes de conjunto de filas cuando captura los datos de origen de datos y cuando ejecuta las instrucciones update posicionadas.  
  
 Cuando la biblioteca de cursores actualiza su caché de los búferes de conjunto de filas, transfiere los datos según el tipo de datos de C especificado en **SQLBindCol**. Por ejemplo, si el tipo de datos de C de un búfer de conjunto de filas es SQL_C_SLONG, la biblioteca de cursores transfiere cuatro bytes de datos; Si es SQL_C_CHAR y *BufferLength* es 10, la biblioteca de cursores transfiere 10 bytes de datos. La biblioteca de cursores no lleva a cabo ninguna comprobación de tipos o conversiones sobre los datos que transfiere.  
  
> [!NOTE]  
>  La biblioteca de cursores no actualiza su caché para una columna si **StrLen_or_IndPtr* en el conjunto de filas correspondiente búfer es SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC.  
  
 Cuando actualiza una columna, datos de caracteres de longitud fija de espacio en blanco rellena de origen de datos y datos binarios de longitud fija rellena hacia cero según sea necesario. Por ejemplo, un origen de datos almacena "Smith" en una columna char (10) como "Smith". La biblioteca de cursores no datos no rellenar espacio en blanco o con ceros en los búferes de conjunto de filas cuando copia estos datos a su memoria caché después de ejecutar una instrucción update posicionadas. Por lo tanto, si una aplicación requiere que los valores en memoria caché de la biblioteca de cursores son rellenada con caracteres de espacio en blanco o con ceros, deben rellenar espacio en blanco o con ceros los valores de los búferes de conjunto de filas antes de ejecutar una instrucción update posicionadas.
