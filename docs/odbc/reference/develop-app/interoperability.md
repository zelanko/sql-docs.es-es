---
title: Interoperabilidad ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b20a696c601ff91c591e4c717f468beca34e36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306226"
---
# <a name="interoperability"></a>Interoperabilidad
*La interoperabilidad* es la capacidad de una sola aplicación para funcionar con muchos DBMS diferentes. La necesidad de escribir aplicaciones genéricas e interoperables fue uno de los principales factores que llevaron al desarrollo de ODBC. Sin embargo, la interoperabilidad no es una ruta simple seguida de "no interoperable" a "completamente interoperable." La ruta de acceso tiene muchas ramas, y cada una requiere compensaciones entre las características, la velocidad, la complejidad del código y el tiempo de desarrollo.  
  
 El proceso de escritura de una aplicación interoperable sigue varios pasos:  
  
1.  Decidir si la aplicación usará ODBC.  
  
2.  Elegir un nivel de interoperabilidad y decidir qué compensaciones son necesarias para alcanzar ese nivel.  
  
3.  Escribir código interoperable y probarlo lo más completo posible.  
  
 Cabe señalar que la interoperabilidad es principalmente el dominio del escritor de aplicaciones. Los controladores están diseñados para trabajar con un único DBMS y, por definición, no son interoperables. Desempeñan un papel en la interoperabilidad al implementar y exponer correctamente ODBC en un único DBMS.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Es la respuesta ODBC?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Elección de un nivel de interoperabilidad](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinar el DBMS de destino y los controladores](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Teniendo en cuenta las características de base de datos que se utilizan](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Longitud del ciclo del producto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Escribir una aplicación Interoperable](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Probar aplicaciones interoperables](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
