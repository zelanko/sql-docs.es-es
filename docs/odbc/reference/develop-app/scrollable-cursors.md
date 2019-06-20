---
title: Los cursores desplazables | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80be6994c7094b365bc24dd135bdda6ec4e561ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468391"
---
# <a name="scrollable-cursors"></a>Cursores desplazables
En las aplicaciones modernas basadas en pantalla, el usuario se desplaza hacia atrás y hacia delante a través de los datos. Para tales aplicaciones, devolver a una fila capturada anteriormente es un problema. Una posibilidad consiste en Cerrar y volver a abrir el cursor y, a continuación, recuperar las filas hasta que llega a la fila requiere el cursor. Otra posibilidad consiste en leer el conjunto de resultados, lo almacena en caché localmente e implementar el desplazamiento en la aplicación. Ambas posibilidades bien solo funcionan con conjuntos de resultados pequeños y la posibilidad de este última es difícil de implementar. Una solución mejor es usar un *cursor desplazable,* que puede avanzar y retroceder en el conjunto de resultados.  
  
 Un *cursor desplazable* se usa normalmente en aplicaciones modernas basadas en pantalla en la que el usuario desplaza hacia delante y hacia atrás a través de los datos. Sin embargo, las aplicaciones deben usar los cursores desplazables solo cuando los cursores de solo avance no realizará el trabajo, como los cursores desplazables son generalmente más caros que los cursores de solo avance.  
  
 La capacidad de retroceder plantea una pregunta no se aplica a los cursores de solo avance: ¿Un cursor desplazable debe detectar los cambios realizados en las filas recuperadas previamente? ¿Es decir, que debe detectar las filas actualizadas, recién insertadas y eliminadas?  
  
 Esta pregunta se produce porque la definición de un conjunto de resultados: el conjunto de filas que coinciden con determinados criterios - no se expone cuando las filas se comprueban para ver si coinciden con ese criterio, ni tampoco si filas deben contener los mismos datos cada vez que se han capturado de estado. La omisión anterior hace posible para los cursores desplazables detectar si las filas se han insertado o eliminado, aunque esto último hace les permite detectar datos actualizados.  
  
 La capacidad para detectar los cambios a veces es útil, a veces no. Por ejemplo, una aplicación de contabilidad necesita un cursor que se pasa por alto todos los cambios; los libros en pantalla de equilibrio es imposible si el cursor muestra los cambios más recientes. Por otro lado, un sistema de reserva de la línea aérea necesita un cursor que muestra los últimos cambios a los datos; Sin este tipo de cursor, debe requery continuamente la base de datos para mostrar la disponibilidad de vuelos más actualizada.  
  
 Para cubrir las necesidades de diferentes aplicaciones, ODBC define cuatro tipos diferentes de los cursores desplazables. Estos cursores varían en gastos y en su capacidad para detectar cambios en el resultado. Tenga en cuenta que si un cursor desplazable puede detectar cambios en filas, solo puede detectar ellos cuando intenta volver a obtener las filas; No hay ninguna manera para el origen de datos notificar al cursor las modificaciones a las filas actualmente capturadas. Tenga en cuenta también que la visibilidad de los cambios también se controla mediante el nivel de aislamiento de transacción; Para obtener más información, consulte [aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de Cursor desplazable](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Uso de los cursores desplazables](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Desplazamiento relativas y absolutas](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
