---
title: Teniendo en cuenta las características de base de datos que se utilizan | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f879d11b4c9f393accaaf96beda6a159aec2363f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="considering-database-features-to-use"></a>Teniendo en cuenta las características de base de datos que se utilizan
Después de que se conoce el nivel básico de interoperabilidad, deben tener en cuenta las características de base de datos usadas por la aplicación. Por ejemplo, ¿qué instrucciones SQL ejecutará la aplicación? ¿La aplicación usará los cursores desplazables? ¿Transacciones? ¿Procedimientos? ¿Datos de tipo Long? Para una idea de qué características podría no admitir todos los DBMS, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) ydescripcionesdefunción[ Apéndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Las características requeridas por una aplicación podrían eliminar algunos de los DBMS en la lista de DBMS de destino. También podría mostrar que la aplicación puede fácilmente tener como destino muchos DBMS.  
  
 Por ejemplo, si las características necesarias son simples, normalmente puede implementar con un alto grado de interoperabilidad. Una aplicación que se ejecuta un sencillo **seleccione** instrucción y recupera los resultados con un cursor de sólo avance es probable que sea muy interoperable en virtud de su sencillez: casi todos los controladores y DBMS admiten la funcionalidad es necesario.  
  
 Sin embargo, si las características necesarias son más complejas, como los cursores desplazables, actualización por posición y las instrucciones delete y procedimientos, a menudo se deben realizar ventajas e inconvenientes. Hay varias causas posibles:  
  
-   **Interoperabilidad inferior, más características.** La aplicación incluye las características pero solo funciona con DBMS que las admiten.  
  
-   **Mayor interoperabilidad, menos características.** La aplicación quita las características pero funciona con más de los DBMS.  
  
-   **Mayor interoperabilidad, características opcionales.** La aplicación incluye las características, pero hace que estén disponibles solo con los DBMS que las admiten.  
  
-   **Mayor interoperabilidad, más características.** La aplicación usa las características con DBMS que admiten y emula ellos para DBMS que no lo hacen.  
  
 Los dos primeros casos son relativamente fáciles de implementar, porque las características se utilizan con todos los DBMS compatibles o con ninguna. Por otro lado, los dos últimos casos, son más complejos. Es necesario en ambos casos para comprobar si el DBMS admite las características y en el último caso para escribir una cantidad potencialmente grande de código para emular estas características. Por lo tanto, estos esquemas están probables que se necesite más tiempo de desarrollo y pueden ser más lentos en tiempo de ejecución.  
  
 Considere la posibilidad de una aplicación de consultas genérico que puede conectarse a un origen de datos único. La aplicación acepta una consulta del usuario y muestra los resultados en una ventana. Ahora suponga que esta aplicación tiene una característica que permite a los usuarios mostrar los resultados de varias consultas simultáneamente. Es decir, puede ejecutar una consulta y examine algunos de los resultados, ejecute una consulta diferente y examinar algunas de sus resultados y, a continuación, volver a la primera consulta. Esto supone un problema de interoperabilidad porque algunos controladores son compatibles con una única instrucción activa.  
  
 La aplicación tiene un número de opciones, según lo que devuelve el controlador de la opción SQL_MAX_CONCURRENT_ACTIVITIES de **SQLGetInfo**:  
  
-   **Siempre se admiten varias consultas.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. Si el controlador admite solo una instrucción activa, la aplicación cierra la conexión y notifica al usuario que el controlador no admite la funcionalidad necesaria. La aplicación es fácil de implementar y ofrece toda la funcionalidad, pero tiene interoperabilidad inferior.  
  
-   **Nunca admite varias consultas.** La aplicación quita por completo la característica. Es fácil de implementar y tiene interoperabilidad alta pero tiene menos funcionalidad.  
  
-   **Admite varias consultas solo si el controlador hace.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación permite al usuario iniciar una nueva instrucción cuando uno ya está activa sólo si el controlador es compatible con varias instrucciones activas. La aplicación tiene mayor funcionalidad y la interoperabilidad, pero es más difícil de implementar.  
  
-   **Siempre admite varias consultas y emular ellos cuando sea necesario.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación siempre permite al usuario iniciar una nueva instrucción cuando uno ya está activa. Si el controlador admite solo una instrucción activa, la aplicación abre una conexión adicional a ese controlador y ejecuta la instrucción nuevo en esa conexión. La aplicación tiene una funcionalidad completa y la interoperabilidad alta, pero es más difícil de implementar.
