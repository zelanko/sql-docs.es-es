---
title: Teniendo en cuenta las características de base de datos que se usarán | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92eeb64b95d666b15c03c70d656d2309a63eabf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042191"
---
# <a name="considering-database-features-to-use"></a>Teniendo en cuenta las características de base de datos que se utilizan
Una vez que se conoce el nivel básico de interoperabilidad, se deben considerar las características de base de datos usadas por la aplicación. Por ejemplo, ¿qué instrucciones SQL ejecutará la aplicación? ¿La aplicación van a usar los cursores desplazables? ¿Transacciones? ¿Procedimientos? ¿Datos de tipo Long? Para ideas acerca de las características que no es posible que sea compatible con todos los DBMS, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descripciones de las funciones y [ Apéndice C: Gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Las características necesarias para una aplicación podrían eliminar algunos de los DBMS en la lista de DBMS de destino. También es posible que muestran que la aplicación puede tener como destino muchos DBMS.  
  
 Por ejemplo, si las características necesarias son sencillas, normalmente se pueden implementar con un alto grado de interoperabilidad. Una aplicación que se ejecuta un sencillo **seleccione** instrucción y recupera los resultados con un cursor de solo avance es probable que sea muy interoperable en virtud de su sencillez: Casi todos los controladores y DBMS admiten la funcionalidad que necesita.  
  
 Sin embargo, si las características necesarias son más complejas, como los cursores desplazables, actualización posicionada y las instrucciones delete y procedimientos, a menudo se deben realizar equilibrios. Hay varias causas posibles:  
  
-   **Interoperabilidad menor, más características.** La aplicación incluye las características, pero solo funciona con los DBMS que las admiten.  
  
-   **Mayor interoperabilidad, menos características.** La aplicación quita las características, pero funciona con más de los DBMS.  
  
-   **Mayor interoperabilidad, características opcionales.** La aplicación incluye las características, pero hace que estén disponibles únicamente con los DBMS que las admiten.  
  
-   **Mayor interoperabilidad, más características.** La aplicación usa las características con los DBMS que los respaldan y emula ellos para DBMS que no lo hacen.  
  
 Los dos primeros casos son relativamente fáciles de implementar, porque las características que se usan con todos los DBMS admitidos o con ninguna. Los dos últimos casos, por otro lado, son más complejos. Es necesario en ambos casos para comprobar si el DBMS es compatible con las características y en el último caso para escribir una cantidad potencialmente grande de código para emular estas características. Por lo tanto, estos esquemas están probables que requieran más tiempo de desarrollo y pueden ser más lentos en tiempo de ejecución.  
  
 Considere la posibilidad de una aplicación de consultas genérico que puede conectarse a un único origen de datos. La aplicación acepta una consulta del usuario y muestra los resultados en una ventana. Ahora supongamos que esta aplicación tiene una característica que permite a los usuarios mostrar los resultados de varias consultas simultáneamente. Es decir, puede ejecutar una consulta y examine algunos de los resultados, ejecutar una consulta diferente y Examinemos algunas de sus resultados y, a continuación, volver a la primera consulta. Esto supone un problema de interoperabilidad porque algunos controladores son compatibles con una única instrucción activa.  
  
 La aplicación tiene una serie de opciones, según lo que devuelve el controlador para la opción SQL_MAX_CONCURRENT_ACTIVITIES en **SQLGetInfo**:  
  
-   **Siempre admite varias consultas.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. Si el controlador admite solo una instrucción activa, la aplicación cierra la conexión e informa al usuario que el controlador no admite la funcionalidad necesaria. La aplicación es fácil de implementar y ofrece toda la funcionalidad, pero tiene interoperabilidad inferior.  
  
-   **Nunca admite varias consultas.** La aplicación quita completamente la característica. Es fácil de implementar y tiene gran interoperabilidad pero tiene menos funcionalidad.  
  
-   **Admite varias consultas solo si el controlador realiza.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación permite al usuario iniciar una nueva instrucción cuando uno está ya activo solo si el controlador es compatible con varias instrucciones activas. La aplicación tiene mayor funcionalidad y la interoperabilidad, pero es más difícil de implementar.  
  
-   **Siempre admite varias consultas y emularlas cuando sea necesario.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación siempre permite al usuario iniciar una nueva instrucción cuando uno ya está activa. Si el controlador admite solo una instrucción activa, la aplicación abre una conexión adicional a ese controlador y la nueva instrucción ejecuta en esa conexión. La aplicación tiene una funcionalidad completa y la interoperabilidad alta, pero es más difícil de implementar.
