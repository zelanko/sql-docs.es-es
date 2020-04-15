---
title: Teniendo en cuenta las características de la base de datos que se va a utilizar . Microsoft Docs
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
ms.openlocfilehash: a9d966781def1c3eab6a9568eab07ab591326171
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299015"
---
# <a name="considering-database-features-to-use"></a>Teniendo en cuenta las características de base de datos que se utilizan
Una vez conocido el nivel básico de interoperabilidad, se deben tener en cuenta las características de base de datos utilizadas por la aplicación. Por ejemplo, ¿qué instrucciones SQL ejecutará la aplicación? ¿Utilizará la aplicación cursores desplazables? ¿Transacciones? ¿Procedimientos? ¿Datos largos? Para obtener ideas sobre qué características podrían no ser compatibles con todos los DBMS, vea las descripciones de las funciones [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)y [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) y [Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Las características requeridas por una aplicación pueden eliminar algunos DBMS de la lista de DBMS de destino. También pueden mostrar que la aplicación puede dirigirse fácilmente a muchos DBMS.  
  
 Por ejemplo, si las características necesarias son simples, normalmente se pueden implementar con un alto grado de interoperabilidad. Una aplicación que ejecuta una simple instrucción **SELECT** y recupera resultados con un cursor de solo avance es probable que sea altamente interoperable en virtud de su simplicidad: casi todos los controladores y DBMS admiten la funcionalidad que necesita.  
  
 Sin embargo, si las características necesarias son más complejas, como cursores desplazables, instrucciones de actualización y eliminación posicionadas y procedimientos, a menudo se deben realizar compensaciones. Hay varias causas posibles:  
  
-   **Menor interoperabilidad, más características.** La aplicación incluye las características, pero solo funciona con DBMS que las admiten.  
  
-   **Mayor interoperabilidad, menos características.** La aplicación elimina las características, pero funciona con más DBMS.  
  
-   **Mayor interoperabilidad, características opcionales.** La aplicación incluye las características, pero las pone a disposición solo con los DBMS que las admiten.  
  
-   **Mayor interoperabilidad, más características.** La aplicación utiliza las características con DBMS que los admiten y los emula para los DBMS que no lo hacen.  
  
 Los dos primeros casos son relativamente fáciles de implementar, ya que las características se utilizan con todos los DBMS admitidos o con ninguno. Estos dos últimos casos, por otra parte, son más complejos. En ambos casos, es necesario comprobar si el DBMS admite las características y, en el último caso, escribir una cantidad potencialmente grande de código para emular estas características. Por lo tanto, es probable que estos esquemas requieran más tiempo de desarrollo y pueden ser más lentos en tiempo de ejecución.  
  
 Considere una aplicación de consulta genérica que pueda conectarse a un único origen de datos. La aplicación acepta una consulta del usuario y muestra los resultados en una ventana. Ahora supongamos que esta aplicación tiene una característica que permite a los usuarios mostrar los resultados de varias consultas simultáneamente. Es decir, pueden ejecutar una consulta y examinar algunos de los resultados, ejecutar una consulta diferente y examinar algunos de sus resultados y, a continuación, volver a la primera consulta. Esto presenta un problema de interoperabilidad porque algunos controladores admiten solo una sola instrucción activa.  
  
 La aplicación tiene una serie de opciones, en función de lo que devuelve el controlador para la opción SQL_MAX_CONCURRENT_ACTIVITIES en **SQLGetInfo**:  
  
-   **Siempre admite varias consultas.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. Si el controlador solo admite una instrucción activa, la aplicación cierra la conexión e informa al usuario de que el controlador no admite la funcionalidad necesaria. La aplicación es fácil de implementar y tiene funcionalidad completa, pero tiene menor interoperabilidad.  
  
-   **Nunca admita varias consultas.** La aplicación elimina la característica por completo. Es fácil de implementar y tiene alta interoperabilidad, pero tiene menos funcionalidad.  
  
-   **Admite varias consultas solo si el controlador lo hace.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación permite al usuario iniciar una nueva instrucción cuando una ya está activa solo si el controlador admite varias instrucciones activas. La aplicación tiene mayor funcionalidad e interoperabilidad, pero es más difícil de implementar.  
  
-   **Siempre admita varias consultas y emulelelas cuando sea necesario.** Después de conectarse a un controlador, la aplicación comprueba el número de instrucciones activas. La aplicación siempre permite al usuario iniciar una nueva instrucción cuando una ya está activa. Si el controlador solo admite una instrucción active, la aplicación abre una conexión adicional a ese controlador y ejecuta la nueva instrucción en esa conexión. La aplicación tiene funcionalidad completa y alta interoperabilidad, pero es más difícil de implementar.
