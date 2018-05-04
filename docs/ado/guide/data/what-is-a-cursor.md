---
title: ¿Qué es un Cursor? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b2f3311063c0a4aac92acaa6054b9f320c3754e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="what-is-a-cursor"></a>¿Qué es un Cursor?
Las operaciones de una base de datos relacional actúan en un conjunto completo de filas. El conjunto de filas que devuelve una instrucción SELECT está compuesto por todas las filas que satisfacen las condiciones de la cláusula WHERE de la instrucción. Este conjunto completo de filas que devuelve la instrucción se conoce como conjunto de resultados. Aplicaciones, especialmente aquellas que son interactivos y en línea, no siempre pueden trabajar eficazmente con el resultado completo como una unidad. Estas aplicaciones necesitan un mecanismo que trabaje con una fila o un pequeño bloque de filas cada vez. Los cursores son una extensión de los conjuntos de resultados que proporcionan dicho mecanismo.  
  
 Un cursor se implementa mediante una biblioteca de cursores. Una biblioteca de cursores es software, a menudo se implementan como parte de un sistema de base de datos o una API, acceso a los datos que se usa para administrar los atributos de los datos devueltos desde un origen de datos (un conjunto de resultados). Estos atributos incluyen la administración de simultaneidad, la posición en el conjunto de resultados, se devuelve el número de filas y si puede mover hacia delante o hacia atrás (o ambos) mediante el resultado configurar (desplazamiento).  
  
 Un cursor realiza un seguimiento de la posición del conjunto de resultados y permite realizar varias operaciones fila por fila en un conjunto de resultados, con o sin devolver a la tabla original. En otras palabras, los cursores devuelven conceptualmente un conjunto de resultados basado en las tablas de las bases de datos. El cursor se denomina así porque indica la posición actual en el conjunto de resultados, igual que el cursor en la pantalla de un equipo indica la posición actual.  
  
 Es importante que se familiarice con el concepto de cursores antes de pasar a aprender los detalles de su uso en ADO.  
  
 Con los cursores, puede:  
  
-   Especifique situarse en filas específicas del conjunto de resultados.  
  
-   Recuperar una fila o un bloque de filas basándose en la posición actual del conjunto de resultados.  
  
-   Modificar los datos de las filas en la posición actual del conjunto de resultados.  
  
-   Definen los distintos niveles de sensibilidad a los cambios de datos realizados por otros usuarios.  
  
 Por ejemplo, considere una aplicación que muestra una lista de productos disponibles para un posible comprador. El comprador se desplaza a través de la lista para ver el costo y los detalles de producto y, por último, selecciona un producto para su compra. Desplazamientos y selecciones adicionales se produce para el resto de la lista. En lo que se refiere al comprador, los productos aparecen uno en uno, pero la aplicación utiliza un cursor desplazable para desplazarse hacia arriba y hacia abajo por el conjunto de resultados.  
  
 Puede utilizar los cursores de varias maneras:  
  
-   Con ninguna fila en absoluto.  
  
-   Con algunas o todas las filas en una sola tabla.  
  
-   Con algunas o todas las filas de tablas unidas lógicamente.  
  
-   Como solo lectura o actualizables en el nivel de cursor o de campo.  
  
-   Como de solo avance o con desplazamiento completo.  
  
-   Con el conjunto de claves de cursor ubicado en el servidor.  
  
-   Sensibles a los cambios en las tablas subyacentes ocasionados por otras aplicaciones (como pertenencia, ordenación, inserciones, actualizaciones y eliminaciones).  
  
-   Existentes en el servidor o el cliente.  
  
 Los cursores de solo lectura, ayudar a los usuarios desplazarse por el conjunto de resultados y los cursores pueden implementar actualizaciones en filas individuales de lectura/escritura. Cursores complejos pueden definirse con conjuntos de claves que señalan a filas de tablas base. Aunque algunos cursores son de solo lectura en una dirección hacia delante, otros usuarios pueden avanzar o retroceder y proporcionar una actualización dinámica del conjunto de resultados según los cambios realizados por otras aplicaciones en la base de datos.  
  
 No todas las aplicaciones deben usar cursores para acceder o actualizar datos. Algunas consultas simplemente no requieren actualización directa de filas mediante un cursor. Los cursores deben ser una de las últimas técnicas empleadas para recuperar datos, y, a continuación, debe elegir el cursor de menor impacto posible. Cuando se crea un conjunto de resultados, mediante un procedimiento almacenado, el conjunto de resultados no es actualizable con cursor editar o métodos de actualización.  
  
## <a name="concurrency"></a>Simultaneidad  
 En algunas aplicaciones multiusuario es muy importante para los datos presentados al usuario final sea tan actualizados como sea posible. Un ejemplo clásico de un sistema de este tipo es un sistema de reserva airline, donde muchos usuarios podrían ser compitiendo por el mismo puesto en un vuelo determinado (y por lo tanto, un único registro). En un caso así, el diseño de la aplicación debe controlar las operaciones simultáneas en un único registro.  
  
 En otras aplicaciones, no es tan importante la simultaneidad. En tales casos, no se puede justificar el gasto que supone mantener que los datos actualizados en todo momento.  
  
## <a name="position"></a>Posición  
 Un cursor también realiza un seguimiento de la posición actual en un conjunto de resultados. Piense en la posición del cursor como un puntero para el registro actual, de forma similar a la forma en que una matriz puntos de índice en el valor en esa ubicación concreta de la matriz.  
  
## <a name="scrollability"></a>Desplazamiento  
 El tipo de cursor que usa la aplicación también afecta a la capacidad para desplazarse hacia delante y hacia atrás por las filas de un conjunto de resultados; Esto se conoce a veces como posibilidades de desplazamiento. La capacidad de avanzar *y* con versiones anteriores a través de un resultado conjunto aumenta la complejidad del cursor y, por tanto, es más costoso de implementar. Por este motivo, deberá solicitar un cursor con esta funcionalidad solo cuando sea necesario.
