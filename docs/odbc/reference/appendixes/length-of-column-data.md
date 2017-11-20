---
title: Longitud de datos de columna | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ee36dbd04cd60d8b5906abc0248d07f28ff5677
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="length-of-column-data"></a>Longitud de datos de columna
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para cada búfer de longitud/indicador enlazado para el conjunto de resultados con **SQLBindCol**. Usa los valores en estos búferes para construir un **donde** cláusula cuando emula actualización por posición o delete. Actualiza estos búferes de los búferes de conjunto de filas cuando captura los datos de origen de datos y cuando ejecuta las instrucciones update posicionadas.  
  
 Si el tipo C de un búfer de datos es SQL_C_CHAR o SQL_C_BINARY y el valor de longitud/indicador es SQL_NTS, la longitud de cadena de los datos se coloca en el búfer de longitud/indicador.  
  
> [!NOTE]  
>  La biblioteca de cursores no actualiza su caché para una columna si **StrLen_or_IndPtr* en el conjunto de filas correspondiente búfer es SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC.

