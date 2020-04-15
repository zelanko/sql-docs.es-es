---
title: Datos de columna ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff89566efa65c88325d98422fe17788f27d2c8ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306596"
---
# <a name="column-data"></a>Datos de columna
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para cada búfer de datos enlazado al conjunto de resultados con **SQLBindCol**. Utiliza los valores de estos búferes para construir una cláusula **WHERE** cuando emula una instrucción update o delete posicionada. Actualiza estos búferes desde los búferes del conjunto de filas cuando recupera datos del origen de datos y cuando ejecuta instrucciones de actualización posicionadas.  
  
 Cuando la biblioteca de cursores actualiza su caché desde los búferes del conjunto de filas, transfiere los datos según el tipo de datos c especificado en **SQLBindCol**. Por ejemplo, si el tipo de datos C de un búfer de conjunto de filas es SQL_C_SLONG, la biblioteca de cursores transfiere cuatro bytes de datos; si se SQL_C_CHAR y *BufferLength* es 10, la biblioteca de cursores transfiere 10 bytes de datos. La biblioteca de cursores no realiza ninguna comprobación de tipos ni conversiones en los datos que transfiere.  
  
> [!NOTE]  
>  La biblioteca de cursores no actualiza su caché para una columna si **StrLen_or_IndPtr* en el búfer de conjunto de filas correspondiente es SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC.  
  
 Cuando actualiza una columna, un origen de datos en blanco rellena los datos de caracteres de longitud fija y los datos binarios de longitud fija de los pads cero según sea necesario. Por ejemplo, un origen de datos almacena "Smith" en una columna CHAR(10) como "Smith". La biblioteca de cursores no utiliza datos de teclado en blanco o de uso cero en los búferes del conjunto de filas cuando copia estos datos en su caché después de ejecutar una instrucción de actualización posicionada. Por lo tanto, si una aplicación requiere que los valores de la memoria caché de la biblioteca de cursores estén acolchados en blanco o con sin azúcar, debe rellenar los valores de los búferes del conjunto de filas antes de ejecutar una instrucción de actualización colocada.
