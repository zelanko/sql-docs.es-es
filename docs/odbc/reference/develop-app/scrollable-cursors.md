---
title: Cursores desplazables (Scrollable Cursors) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304216"
---
# <a name="scrollable-cursors"></a>Cursores desplazables
En las aplicaciones modernas basadas en pantalla, el usuario se desplaza hacia atrás y hacia adelante a través de los datos. Para este tipo de aplicaciones, volver a una fila previamente recuperada es un problema. Una posibilidad es cerrar y volver a abrir el cursor y, a continuación, capturar filas hasta que el cursor alcanza la fila requerida. Otra posibilidad es leer el conjunto de resultados, almacenarlo en caché localmente e implementar el desplazamiento en la aplicación. Ambas posibilidades funcionan bien sólo con pequeños conjuntos de resultados, y esta última posibilidad es difícil de implementar. Una mejor solución es utilizar un *cursor desplazable,* que puede moverse hacia atrás y hacia adelante en el conjunto de resultados.  
  
 Un *cursor desplazable* se utiliza comúnmente en aplicaciones modernas basadas en pantalla en las que el usuario se desplaza hacia adelante y hacia atrás a través de los datos. Sin embargo, las aplicaciones deben utilizar cursores desplazables solo cuando los cursores de solo avance no realizarán el trabajo, ya que los cursores desplazables suelen ser más caros que los cursores de solo avance.  
  
 La capacidad de retroceder plantea una pregunta que no es aplicable a los cursores de solo avance: ¿Debe un cursor desplazable detectar los cambios realizados en las filas capturadas anteriormente? Es decir, ¿debería detectar filas actualizadas, eliminadas y recién insertadas?  
  
 Esta pregunta surge porque la definición de un conjunto de resultados (el conjunto de filas que coincide con determinados criterios) no indica cuándo se comprueban las filas para ver si coinciden con esos criterios, ni indica si las filas deben contener los mismos datos cada vez que se obtienen. La omisión anterior permite que los cursores desplazables detecten si las filas se han insertado o eliminado, mientras que la segunda les permite detectar datos actualizados.  
  
 La capacidad de detectar cambios a veces es útil, a veces no. Por ejemplo, una aplicación de contabilidad necesita un cursor que ignore todos los cambios; equilibrar los libros es imposible si el cursor muestra los últimos cambios. Por otro lado, un sistema de reserva de aerolíneas necesita un cursor que muestre los últimos cambios en los datos; sin un cursor de este tipo, debe volver a consultar continuamente la base de datos para mostrar la disponibilidad de vuelo más actualizada.  
  
 Para cubrir las necesidades de diferentes aplicaciones, ODBC define cuatro tipos diferentes de cursores desplazables. Estos cursores varían tanto en gastos como en su capacidad para detectar cambios en el conjunto de resultados. Tenga en cuenta que si un cursor desplazable puede detectar cambios en las filas, solo puede detectarlos cuando intenta recuperar esas filas; no hay manera de que el origen de datos notifique al cursor de los cambios en las filas recuperadas actualmente. Tenga en cuenta también que la visibilidad de los cambios también está controlada por el nivel de aislamiento de transacción; Para obtener más información, consulte [Aislamiento de transacciones](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de Cursor desplazable](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Uso de los cursores desplazables](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Desplazamiento relativas y absolutas](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
