---
title: Los cursores desplazables | Documentos de Microsoft
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e779d551385c62ae8cddc5a2e7612b88095497
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="scrollable-cursors"></a>Cursores desplazables
En las aplicaciones modernas basado en pantalla, el usuario se desplaza hacia atrás y hacia delante a través de los datos. Para estas aplicaciones, volver a una fila recopilada previamente es un problema. Una posibilidad es cerrar y volver a abrir el cursor y, a continuación, capturar las filas hasta que el cursor alcanza la fila necesaria. Otra posibilidad consiste en leer el conjunto de resultados, almacenarla en la caché local e implementar el desplazamiento en la aplicación. Ambas posibilidades también solo funcionan con conjuntos de resultados pequeños, y la posibilidad de este última es difícil de implementar. Una solución mejor es usar un *un cursor desplazable,* que puede avanzar y retroceder en el conjunto de resultados.  
  
 A *cursor desplazable* se suele usar en aplicaciones modernas basado en pantalla en el que el usuario se desplaza de y hacia atrás a través de los datos. Sin embargo, aplicaciones deben utilizar los cursores desplazables solo cuando los cursores de solo avance no realizará el trabajo, como los cursores desplazables son generalmente más caros que los cursores de solo avance.  
  
 ¿La capacidad de retroceder genera una pregunta no es aplicable a los cursores de solo avance: un cursor desplazable debe detectar los cambios realizados a filas capturadas anteriormente? ¿Es decir, deberían detectar filas actualizadas, recién insertadas y eliminadas?  
  
 Esta pregunta que surge porque la definición de un resultado de establecer, el conjunto de filas que coincide con determinados criterios, no de estado cuando se comprueban las filas para ver si coincide con ese criterio, ni estado si filas deben contener los mismos datos cada vez que se han capturado. La omisión anterior hace posible para los cursores desplazables detectar si filas se han insertado o eliminado, si bien esto último hace les permite detectar datos actualizados.  
  
 La capacidad para detectar cambios a veces es útil, a veces no. Por ejemplo, una aplicación de contabilidad necesita un cursor que pasa por alto todos los cambios; equilibrio libros resulta imposible si el cursor muestra los cambios más recientes. Por otro lado, un sistema de reserva airline necesita un cursor que muestra los últimos cambios a los datos; Sin este tipo de cursor, debe consultar continuamente la base de datos para mostrar la disponibilidad de vuelo más actualizada.  
  
 Para cubrir las necesidades de distintas aplicaciones, ODBC define cuatro tipos diferentes de los cursores desplazables. Estos cursores varían en gastos y en su capacidad para detectar cambios en el resultado establecido. Tenga en cuenta que si un cursor desplazable puede detectar cambios en filas, solo puede detectar ellos cuando intenta capturar estas filas; No hay ninguna manera de que el origen de datos notificar al cursor las modificaciones realizadas en las filas actualmente capturadas. Tenga en cuenta también que la visibilidad de los cambios también se controla mediante el nivel de aislamiento de transacción; Para obtener más información, consulte [de aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de Cursor desplazable](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Uso de los cursores desplazables](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Desplazamiento relativas y absolutas](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
