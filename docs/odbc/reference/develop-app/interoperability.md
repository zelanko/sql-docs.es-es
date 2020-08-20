---
description: Interoperabilidad
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a404ee6de56cbd8b5605eca640fdf0e065f16d79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476617"
---
# <a name="interoperability"></a>Interoperabilidad
La *interoperabilidad* es la capacidad de una sola aplicación para operar con muchos DBMS diferentes. La necesidad de escribir aplicaciones genéricas interoperables era uno de los principales factores que conducen al desarrollo de ODBC. Sin embargo, la interoperabilidad no es una ruta de acceso simple seguida de "no interoperable" a "completamente interoperable". La ruta de acceso tiene muchas bifurcaciones y cada una de ellas requiere ventajas e inconvenientes entre las características, la velocidad, la complejidad del código y el tiempo de desarrollo.  
  
 El proceso de escritura de una aplicación interoperable sigue varios pasos:  
  
1.  Decidir si la aplicación va a utilizar ODBC.  
  
2.  Elección de un nivel de interoperabilidad y decisión de qué ventajas es necesario para alcanzar ese nivel.  
  
3.  Escribir código interoperable y probarlo lo máximo posible.  
  
 Debe tenerse en cuentan que la interoperabilidad es principalmente el dominio del escritor de la aplicación. Los controladores están diseñados para funcionar con un solo DBMS y, por definición, no son interoperables. Desempeñan un papel en la interoperabilidad implementando y exponiendo ODBC correctamente a través de un DBMS único.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Es la respuesta ODBC?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Elección de un nivel de interoperabilidad](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinar el DBMS de destino y los controladores](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Teniendo en cuenta las características de base de datos que se utilizan](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Longitud del ciclo del producto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Escribir una aplicación Interoperable](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Probar aplicaciones interoperables](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
