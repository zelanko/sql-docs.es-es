---
title: ¿Qué es un Cursor? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], about cursors
ms.assetid: 596eb4b6-c22f-4cde-b23f-172dd66c3161
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9ad683af9cea8ca4f5bc1736a48f0662656b6ef1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704519"
---
# <a name="what-is-a-cursor"></a>¿Qué es un Cursor?
Las operaciones de una base de datos relacional actúan en un conjunto completo de filas. El conjunto de filas que devuelve una instrucción SELECT está compuesto por todas las filas que satisfacen las condiciones de la cláusula WHERE de la instrucción. Este conjunto completo de filas que devuelve la instrucción se conoce como conjunto de resultados. Aplicaciones, especialmente aquellas que son interactivas y en línea, no siempre pueden trabajar eficazmente con el completo conjunto de resultados como una unidad. Estas aplicaciones necesitan un mecanismo que trabaje con una fila o un pequeño bloque de filas cada vez. Los cursores son una extensión de los conjuntos de resultados que proporcionan dicho mecanismo.  
  
 Un cursor se implementa mediante una biblioteca de cursores. Una biblioteca de cursores es software, a menudo se implementan como parte de un sistema de base de datos o una API, acceso a los datos que se usa para administrar los atributos de los datos devueltos desde un origen de datos (un conjunto de resultados). Estos atributos incluyen la administración de simultaneidad, la posición en el conjunto de resultados, se devuelve el número de filas y si puede mover hacia delante o hacia atrás (o ambos) mediante el resultado establecido (desplazamiento).  
  
 Un cursor realiza un seguimiento de la posición del conjunto de resultados y permite realizar varias operaciones fila por fila en un conjunto de resultados, con o sin volver a la tabla original. En otras palabras, los cursores conceptualmente devuelven un conjunto de resultados basándose en las tablas de las bases de datos. El cursor se denomina así porque indica la posición actual en el conjunto de resultados, igual que el cursor en la pantalla indica la posición actual.  
  
 Es importante familiarizarse con el concepto de cursores antes de pasar a aprender los detalles de su uso en ADO.  
  
 Los cursores de hacer lo siguiente:  
  
-   Especificar la posición en filas específicas del conjunto de resultados.  
  
-   Recuperar una fila o un bloque de filas basándose en la posición del conjunto de resultados actual.  
  
-   Modificar los datos de las filas en la posición actual del conjunto de resultados.  
  
-   Definir diferentes niveles de sensibilidad a los cambios de datos realizados por otros usuarios.  
  
 Por ejemplo, considere una aplicación que muestra una lista de productos disponibles para un posible comprador. El comprador se desplaza por la lista para ver el costo y los detalles del producto y, por último, selecciona un producto para su compra. Desplazamiento adicional y la selección se produce durante el resto de la lista. En cuanto se refiere a los compradores, los productos aparecen una vez, pero la aplicación utiliza un cursor desplazable para examinar y reducir verticalmente el conjunto de resultados.  
  
 Puede utilizar cursores en una variedad de formas:  
  
-   Sin filas en absoluto.  
  
-   Con todas o algunas de las filas de una sola tabla.  
  
-   Con algunas o todas las filas de tablas unidas lógicamente.  
  
-   Como solo lectura o actualizables en el nivel de cursor o de campo.  
  
-   Como de solo avance o con desplazamiento completo.  
  
-   Con el cursor de conjunto de claves ubicado en el servidor.  
  
-   Sensibles a los cambios de la tabla subyacente causados por otras aplicaciones (por ejemplo, la pertenencia, ordenación, inserciones, actualizaciones y eliminaciones).  
  
-   Existentes en el servidor o el cliente.  
  
 Los cursores de solo lectura, ayudar a los usuarios examinar el conjunto de resultados y los cursores pueden implementar las actualizaciones de filas individuales de lectura/escritura. Cursores complejos pueden definirse con conjuntos de claves que apuntan a filas de tablas base. Aunque algunos cursores son de solo lectura hacia delante, otros usuarios pueden avanzar o retroceder y proporcionar una actualización dinámica del conjunto de resultados según los cambios que realizan otras aplicaciones de la base de datos.  
  
 No todas las aplicaciones deben usar cursores para acceder o actualizar datos. Algunas consultas simplemente no requieren actualización directa de filas mediante un cursor. Los cursores deben ser una de las últimas técnicas empleadas para recuperar datos- y, a continuación, debe elegir el cursor de menor impacto posible. Cuando se crea un conjunto de resultados, mediante un procedimiento almacenado, el conjunto de resultados no es actualizable con cursor editar o actualizar los métodos.  
  
## <a name="concurrency"></a>Simultaneidad  
 En algunas aplicaciones multiusuario es muy importante para los datos presentados al usuario final sea tan actualizados como sea posible. Un ejemplo clásico de este sistema es un sistema de reserva de líneas aéreas, donde muchos usuarios podrían ser compiten por el mismo asiento en un vuelo determinado (y por lo tanto, un único registro). En un caso como éste, el diseño de la aplicación debe controlar las operaciones simultáneas en un único registro.  
  
 En otras aplicaciones, la simultaneidad no es tan importante. En tales casos, no se puede justificar el gasto que supone mantener que los datos actualizados en todo momento.  
  
## <a name="position"></a>Posición  
 Un cursor también realiza un seguimiento de la posición actual en un conjunto de resultados. Pensar en la posición del cursor como un puntero para el registro actual, similar a la forma en una matriz de puntos de índice en el valor en esa ubicación concreta de la matriz.  
  
## <a name="scrollability"></a>Desplazamiento  
 El tipo de cursor que usa la aplicación también afecta a la capacidad para desplazarse hacia delante y hacia atrás por las filas de un conjunto de resultados; Esto se denomina a veces posibilidades de desplazamiento. La capacidad de desplazarse hacia delante *y* con versiones anteriores a través de un resultado conjunto aumenta la complejidad del cursor y, por lo tanto, es más costosa de implementar. Por este motivo, debe pedir un cursor con esta funcionalidad solo cuando sea necesario.
