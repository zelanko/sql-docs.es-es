---
description: Cursores desplazables
title: Cursores desplazables | Microsoft Docs
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
ms.openlocfilehash: 9c347dcb130a2f1f899f2e1b83ae28289ff0a923
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476487"
---
# <a name="scrollable-cursors"></a>Cursores desplazables
En modernas aplicaciones basadas en pantalla, el usuario se desplaza hacia atrás y hacia delante por los datos. Para estas aplicaciones, el hecho de volver a una fila capturada previamente es un problema. Una posibilidad es cerrar y volver a abrir el cursor y, a continuación, capturar filas hasta que el cursor alcance la fila requerida. Otra posibilidad es leer el conjunto de resultados, almacenarlo en caché localmente e implementar el desplazamiento en la aplicación. Ambas posibilidades funcionan bien solo con conjuntos de resultados pequeños y la segunda posibilidad es difícil de implementar. Una solución mejor es usar un *cursor desplazable,* que puede moverse hacia atrás y hacia delante en el conjunto de resultados.  
  
 Un *cursor desplazable* se usa normalmente en aplicaciones modernas basadas en pantallas en las que el usuario se desplaza hacia atrás y hacia delante por los datos. Sin embargo, las aplicaciones deben usar cursores desplazables solo cuando los cursores de solo avance no realizarán el trabajo, ya que los cursores desplazables suelen ser más caros que los cursores de solo avance.  
  
 La capacidad de desplazarse hacia atrás genera una pregunta que no es aplicable a los cursores de solo avance: ¿un cursor desplazable detecta los cambios realizados en las filas capturadas anteriormente? Es decir, ¿debe detectar las filas actualizadas, eliminadas y recién insertadas?  
  
 Esta pregunta se produce porque la definición de un conjunto de resultados (el conjunto de filas que coincide con determinados criterios) no indica cuándo se comprueban las filas para ver si coinciden con los criterios, ni tampoco el estado si las filas deben contener los mismos datos cada vez que se capturan. La omisión anterior permite que los cursores desplazables detecten si se han insertado o eliminado filas, mientras que la segunda permite que detecten datos actualizados.  
  
 La capacidad de detectar cambios es a veces útil, a veces no. Por ejemplo, una aplicación de contabilidad necesita un cursor que omita todos los cambios; no es posible equilibrar los libros si el cursor muestra los últimos cambios. Por otro lado, un sistema de reserva de una línea aérea necesita un cursor que muestra los últimos cambios de los datos. sin este tipo de cursor, debe reconsultar continuamente la base de datos para mostrar la disponibilidad de vuelo más actualizada.  
  
 Para cubrir las necesidades de distintas aplicaciones, ODBC define cuatro tipos diferentes de cursores desplazables. Estos cursores varían tanto en gastos como en su capacidad para detectar cambios en el conjunto de resultados. Tenga en cuenta que si un cursor desplazable puede detectar cambios en las filas, solo podrá detectarlos cuando intente volver a capturar esas filas; no hay ninguna manera de que el origen de datos notifique al cursor los cambios en las filas capturadas actualmente. Tenga en cuenta también que la visibilidad de los cambios también se controla mediante el nivel de aislamiento de transacción; para obtener más información, vea [aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de Cursor desplazable](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Uso de los cursores desplazables](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Desplazamiento relativas y absolutas](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md)
