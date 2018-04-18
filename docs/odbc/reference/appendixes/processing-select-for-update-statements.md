---
title: Procesamiento SELECT para las instrucciones UPDATE | Documentos de Microsoft
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
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c1af5a6c3bdd4a04f0d901158643e29d40962a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="processing-select-for-update-statements"></a>Seleccione para instrucciones UPDATE de procesamiento
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Para obtener una interoperabilidad máxima, las aplicaciones deben generar conjuntos de resultados que se actualiza con una instrucción update posicionadas mediante la ejecución de un **seleccione para actualizar** instrucción. Aunque la biblioteca de cursores no requiere esto, es necesario por la mayoría de los orígenes de datos que admiten las instrucciones update posicionadas.  
  
 La biblioteca de cursores pasa por alto las columnas de la **FOR UPDATE** cláusula de una **SELECT FOR UPDATE** instrucción; esta cláusula quita antes de pasar la instrucción del controlador. En la biblioteca de cursores, el atributo de instrucción SQL_ATTR_CONCURRENCY, junto con las restricciones mencionadas en la sección anterior, controles si las columnas en un resultado de conjunto se pueden actualizar.
