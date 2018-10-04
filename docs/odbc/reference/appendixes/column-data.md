---
title: Datos de columna | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95f80c82d3804e31d5ea29d55af0fbedd4184e6c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695163"
---
# <a name="column-data"></a>Datos de columna
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para cada búfer de datos enlazado en el conjunto de resultados con **SQLBindCol**. Lo utiliza los valores de estos búferes para construir un **donde** cláusula cuando emula una posición instrucción update o delete. Cuando recupera los datos de origen de datos y cuando ejecuta las instrucciones update posicionadas actualiza estos búferes de los búferes de conjunto de filas.  
  
 Cuando la biblioteca de cursores actualiza su caché de los búferes de conjunto de filas, transfiere los datos según el tipo de datos C especificado en **SQLBindCol**. Por ejemplo, si el tipo de datos C de un búfer de conjunto de filas es SQL_C_SLONG, la biblioteca de cursores transfiere cuatro bytes de datos. Si es SQL_C_CHAR y *BufferLength* es 10, la biblioteca de cursores transfiere 10 bytes de datos. La biblioteca de cursores no lleva a cabo ninguna comprobación de tipos o conversiones sobre los datos que transfiere.  
  
> [!NOTE]  
>  La biblioteca de cursores no actualiza su caché para una columna si **StrLen_or_IndPtr* en el conjunto de filas correspondiente búfer es SQL_DATA_AT_EXEC ni el resultado de la macro SQL_LEN_DATA_AT_EXEC.  
  
 Cuando actualiza una columna, datos de caracteres de longitud fija de paneles de espacio en blanco de origen de datos y datos binarios de longitud fija de cero paneles según sea necesario. Por ejemplo, un origen de datos almacena "Smith" en una columna char (10) como "Smith". La biblioteca de cursores no datos no pad de espacio en blanco o con ceros en los búferes de conjunto de filas cuando copiará estos datos a su memoria caché después de ejecutar una instrucción de actualización posicionada. Por lo tanto, si una aplicación requiere que los valores en memoria caché de la biblioteca de cursores son rellenada con caracteres de espacio en blanco o con ceros, deben rellenar en blanco o con ceros los valores de los búferes de conjunto de filas antes de ejecutar una instrucción de actualización posicionada.
