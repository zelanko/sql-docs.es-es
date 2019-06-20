---
title: Interoperabilidad | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d5e4fbee458bec88461d3e2945a466c848d3345
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446492"
---
# <a name="interoperability"></a>Interoperabilidad
*Interoperabilidad* es la capacidad de una sola aplicación para que funcione con muchos DBMS diferentes. La necesidad de escribir aplicaciones interoperables genéricas fue uno de los principales factores que conducen al desarrollo de ODBC. Sin embargo, interoperabilidad no es una ruta de acceso simple seguido de "no es interoperable" a "completamente interoperable". La ruta de acceso tiene muchas bifurcaciones y cada uno requiere equilibrios entre características, velocidad, complejidad del código y el tiempo de desarrollo.  
  
 El proceso de escribir una aplicación interoperable sigue varios pasos:  
  
1.  Decidir si la aplicación usará ODBC.  
  
2.  Elegir un nivel de interoperabilidad y decidir qué ventajas y desventajas son necesarios para llegar a ese nivel.  
  
3.  Escribir código interoperable y su prueba más completa posible.  
  
 Debe tenerse en cuenta que la interoperabilidad es principalmente el dominio de la escritura de la aplicación. Los controladores están diseñados para funcionar con un DBMS único y, por definición, no son interoperables. Juegan un rol en interoperabilidad implementando correctamente y exposición de ODBC a través de un DBMS único.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Es la respuesta ODBC?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Elección de un nivel de interoperabilidad](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinar el DBMS de destino y los controladores](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Teniendo en cuenta las características de base de datos que se utilizan](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Longitud del ciclo del producto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Escribir una aplicación Interoperable](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Probar aplicaciones interoperables](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
