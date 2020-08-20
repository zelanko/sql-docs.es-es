---
description: Teniendo en cuenta las características de base de datos que se utilizan
title: Consideraciones de uso de las características de base de datos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2abaed3806514a161c5c506d8bad89b4d3b75153
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465897"
---
# <a name="considering-database-features-to-use"></a>Teniendo en cuenta las características de base de datos que se utilizan
Una vez conocido el nivel básico de interoperabilidad, se deben tener en cuenta las características de base de datos utilizadas por la aplicación. Por ejemplo, ¿qué instrucciones SQL ejecutará la aplicación? ¿Usará la aplicación cursores desplazables? Realizadas? Procedimientos? ¿Datos largos? Para obtener ideas sobre las características que pueden no admitir todos los DBMS, vea las descripciones de las funciones [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) , y el [Apéndice C: gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Las características requeridas por una aplicación podrían eliminar algunos DBMS de la lista de DBMS de destino. También podrían mostrar que la aplicación puede dirigirse fácilmente a muchos DBMS.  
  
 Por ejemplo, si las características necesarias son simples, normalmente se pueden implementar con un alto grado de interoperabilidad. Una aplicación que ejecuta una instrucción **Select** simple y recupera los resultados con un cursor de solo avance es probable que sea altamente interoperable en virtud de su simplicidad: casi todos los controladores y DBMS admiten la funcionalidad que necesita.  
  
 Sin embargo, si las características necesarias son más complejas, como los cursores desplazables, las instrucciones Update y DELETE posicionadas, y los procedimientos, a menudo se deben realizar ventajas. Hay varias causas posibles:  
  
-   **Menor interoperabilidad, más características.** La aplicación incluye las características, pero solo funciona con DBMS que las admitan.  
  
-   **Mayor interoperabilidad, menos características.** La aplicación quita las características, pero funciona con más DBMS.  
  
-   **Mayor interoperabilidad, características opcionales.** La aplicación incluye las características, pero las pone a disposición solo con los DBMS que las admiten.  
  
-   **Mayor interoperabilidad, más características.** La aplicación utiliza las características de con DBMS que las admiten y las emula para los DBMS que no.  
  
 Los dos primeros casos son relativamente sencillos de implementar, ya que las características se usan con todos los DBMS compatibles o con ninguno. Los dos últimos casos, por otro lado, son más complejos. En ambos casos, es necesario comprobar si DBMS admite las características y, en el último caso, escribir una cantidad de código potencialmente grande para emular estas características. Por lo tanto, es probable que estos esquemas requieran más tiempo de desarrollo y que sean más lentos en tiempo de ejecución.  
  
 Considere una aplicación de consulta genérica que puede conectarse a un único origen de datos. La aplicación acepta una consulta del usuario y muestra los resultados en una ventana. Ahora Supongamos que esta aplicación tiene una característica que permite a los usuarios mostrar los resultados de varias consultas simultáneamente. Es decir, pueden ejecutar una consulta y examinar algunos de los resultados, ejecutar una consulta diferente y examinar algunos de sus resultados y, a continuación, volver a la primera consulta. Esto presenta un problema de interoperabilidad porque algunos controladores solo admiten una única instrucción activa.  
  
 La aplicación tiene varias opciones, en función de lo que devuelve el controlador para la opción SQL_MAX_CONCURRENT_ACTIVITIES en **SQLGetInfo**:  
  
-   **Admita siempre varias consultas.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. Si el controlador solo admite una instrucción activa, la aplicación cierra la conexión e informa al usuario de que el controlador no admite la funcionalidad necesaria. La aplicación es fácil de implementar y tiene funcionalidad completa, pero tiene una menor interoperabilidad.  
  
-   **Nunca admite varias consultas.** La aplicación quita la característica por completo. Es fácil de implementar y tiene una gran interoperabilidad, pero tiene menos funcionalidad.  
  
-   **Solo se admiten varias consultas si el controlador lo hace.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación permite al usuario iniciar una nueva instrucción cuando una ya está activa solo si el controlador admite varias instrucciones activas. La aplicación tiene mayor funcionalidad e interoperabilidad, pero es más difícil de implementar.  
  
-   **Admita siempre varias consultas y eMule cuando sea necesario.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación siempre permite al usuario iniciar una nueva instrucción cuando ya hay una activa. Si el controlador solo admite una instrucción activa, la aplicación abre una conexión adicional a ese controlador y ejecuta la nueva instrucción en esa conexión. La aplicación tiene funcionalidad completa y alta interoperabilidad, pero es más difícil de implementar.
