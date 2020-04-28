---
title: La solución ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b35883ff4d621f0ecc092020ad744455281dd63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286758"
---
# <a name="the-odbc-solution"></a>La solución ODBC
La pregunta, a continuación, ¿cómo estandariza ODBC el acceso a la base de datos? Existen dos requisitos arquitectónicos:  
  
-   Las aplicaciones deben poder tener acceso a varios DBMS mediante el mismo código fuente sin tener que volver a compilar o volver a vincular.  
  
-   Las aplicaciones deben poder tener acceso a varios DBMS simultáneamente.  
  
 Y hay una pregunta más, debido a la realidad de Marketplace:  
  
-   ¿Qué características de DBMS debe exponer ODBC? ¿Solo las características que son comunes a todos los DBMS o a cualquier característica que esté disponible en cualquier DBMS?  
  
 ODBC resuelve estos problemas de la siguiente manera:  
  
-   **ODBC es una interfaz de nivel de llamada.** Para solucionar el problema de cómo las aplicaciones tienen acceso a varios DBMS mediante el mismo código fuente, ODBC define una CLI estándar. Contiene todas las funciones de las especificaciones de la CLI de Open Group e ISO/IEC y proporciona funciones adicionales que las aplicaciones suelen necesitar.  
  
     Se requiere una biblioteca o controlador diferente para cada DBMS que admita ODBC. El controlador implementa las funciones de la API de ODBC. Para usar un controlador diferente, no es necesario volver a compilar o volver a crear el vínculo de la aplicación. En su lugar, la aplicación simplemente carga el nuevo controlador y llama a las funciones que hay en él. Para tener acceso a varios DBMS simultáneamente, la aplicación carga varios controladores. El modo en que se admiten los controladores es específico del sistema operativo. Por ejemplo, en el sistema operativo Microsoft® Windows®, los controladores son bibliotecas de vínculos dinámicos (dll).  
  
-   **ODBC define una gramática estándar de SQL.** Además de una interfaz de nivel de llamada estándar, ODBC define una gramática estándar de SQL. Esta gramática se basa en la especificación CAE de SQL de grupo abierto. Las diferencias entre las dos gramáticas son menores y principalmente debido a las diferencias entre la gramática de SQL requerida por SQL incrustado (Open Group) y una CLI (ODBC). También hay algunas extensiones para la gramática que exponen las características del lenguaje disponible normalmente que no se incluyen en la gramática de Open Group.  
  
     Las aplicaciones pueden enviar instrucciones mediante la gramática específica de ODBC o DBMS. Si una instrucción utiliza una gramática de ODBC diferente de la gramática específica de DBMS, el controlador la convierte antes de enviarla al origen de datos. Sin embargo, estas conversiones son poco frecuentes porque la mayoría de los DBMS ya usan la gramática estándar de SQL.  
  
-   **ODBC proporciona un administrador de controladores para administrar el acceso simultáneo a varios DBMS.** Aunque el uso de controladores resuelve el problema de tener acceso a varios DBMS simultáneamente, el código para hacer esto puede ser complejo. Las aplicaciones que están diseñadas para funcionar con todos los controladores no se pueden vincular estáticamente a ningún controlador. En su lugar, deben cargar los controladores en tiempo de ejecución y llamar a las funciones en ellos a través de una tabla de punteros de función. La situación es más compleja si la aplicación usa varios controladores simultáneamente.  
  
     En lugar de obligar a cada aplicación a hacer esto, ODBC proporciona un administrador de controladores. El administrador de controladores implementa todas las funciones ODBC, principalmente como llamadas de paso a través a las funciones ODBC en los controladores, y se vincula estáticamente a la aplicación o la carga la aplicación en tiempo de ejecución. Por lo tanto, la aplicación llama a las funciones ODBC por nombre en el administrador de controladores, en lugar de mediante un puntero en cada controlador.  
  
     Cuando una aplicación necesita un controlador determinado, primero solicita un identificador de conexión con el que identificar el controlador y, a continuación, solicita que el administrador de controladores cargue el controlador. El administrador de controladores carga el controlador y almacena la dirección de cada función en el controlador. Para llamar a una función ODBC en el controlador, la aplicación llama a esa función en el administrador de controladores y pasa el identificador de conexión para el controlador. A continuación, el administrador de controladores llama a la función mediante la dirección que almacenó anteriormente.  
  
-   **ODBC expone un número significativo de características de DBMS, pero no requiere que los controladores sean compatibles con todas ellas.** Si ODBC solo expone características que son comunes a todos los DBMS, sería de poco uso; después de todo, la razón por la que existen muchos DBMS diferentes hoy es que tienen características diferentes. Si ODBC expone todas las características que están disponibles en cualquier DBMS, no sería posible implementar los controladores.  
  
     En su lugar, ODBC expone un número significativo de características (más que son compatibles con la mayoría de los DBMS), pero requiere que los controladores implementen solo un subconjunto de esas características. Los controladores implementan las características restantes solo si son compatibles con el DBMS subyacente o si optan por emularlas. Por lo tanto, se pueden escribir aplicaciones para que aprovechen las características de un solo DBMS, tal como las expone el controlador para ese DBMS, para usar solo las características usadas por todos los DBMS o para comprobar la compatibilidad de una característica determinada y reaccionar en consecuencia.  
  
     Para que una aplicación pueda determinar qué características admite un controlador y DBMS, ODBC proporciona dos funciones (**SQLGetInfo** y **SQLGetFunctions**) que devuelven información general sobre las capacidades del controlador y DBMS, así como una lista de funciones que admite el controlador. ODBC también define los niveles de cumplimiento de la gramática de SQL y API, que especifican amplios intervalos de características admitidas por el controlador. Para obtener más información, vea [niveles de cumplimiento](../../odbc/reference/develop-app/conformance-levels.md).  
  
     Es importante recordar que ODBC define una interfaz común para todas las características que expone. Por este motivo, las aplicaciones contienen código específico de características, no código específico de DBMS, y pueden usar los controladores que exponen esas características. Una ventaja de esto es que no es necesario actualizar las aplicaciones cuando se mejoran las características admitidas por un DBMS. en su lugar, cuando se instala un controlador actualizado, la aplicación usa automáticamente las características porque su código es específico de la característica, no específico del controlador ni específico del DBMS.
