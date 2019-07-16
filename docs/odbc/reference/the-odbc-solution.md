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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6992e084c210cea1b95157744addfd40180fccb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039341"
---
# <a name="the-odbc-solution"></a>La solución ODBC
¿La cuestión es cómo estandarizar ODBC acceso de la base de datos? Hay dos requisitos de arquitectura:  
  
-   Las aplicaciones deben poder tener acceso a varios DBMS con el mismo código fuente sin volver a compilar o volver a vincular.  
  
-   Las aplicaciones deben poder tener acceso simultáneamente a varios DBMS.  
  
 Y hay una pregunta más, debido a la realidad de marketplace:  
  
-   ¿Qué características DBMS debe exponer ODBC? ¿Solo las características que son comunes a todos los DBMS o cualquier característica que está disponible en cualquier DBMS?  
  
 ODBC soluciona estos problemas de la siguiente manera:  
  
-   **ODBC es una interfaz de nivel de llamada.** Para solucionar el problema de cómo las aplicaciones tener acceso a varios DBMS con el mismo código fuente, ODBC define un estándar de la CLI. Contiene todas las funciones en las especificaciones de la CLI de Open Group y ISO/IEC y proporciona funciones adicionales que requieren habitualmente las aplicaciones.  
  
     Una biblioteca diferente, o el controlador, se requiere para cada DBMS que admite ODBC. El controlador implementa las funciones de la API de ODBC. Para usar un controlador diferente, la aplicación no es necesario volver a compilar y vincular. En su lugar, la aplicación simplemente carga el controlador nuevo y llama a las funciones en ella. Para obtener acceso a varios DBMS al mismo tiempo, la aplicación carga varios controladores. Cómo se admiten los controladores es específico del sistema operativo. Por ejemplo, en el sistema operativo Microsoft® Windows®, los controladores son bibliotecas de vínculos dinámicos (DLL).  
  
-   **ODBC define una gramática SQL estándar.** Además de una interfaz de nivel de llamada estándar, ODBC define una gramática SQL estándar. Esta gramática se basa en la especificación Open Group SQL CAE. Diferencias entre los dos objetos son menores y principalmente debido a las diferencias entre la gramática de SQL requerido embedded SQL (Open Group) y una CLI (ODBC). También hay algunas extensiones a la gramática para exponer las características de lenguaje disponibles habitualmente no cubiertas por la gramática de Open Group.  
  
     Las aplicaciones pueden enviar instrucciones mediante la gramática de ODBC o específicos para DBMS. Si una instrucción usa la gramática ODBC que es diferente de la gramática de DBMS específicos, el controlador lo convierte antes de enviarla al origen de datos. Sin embargo, estas conversiones son poco frecuentes, porque la mayoría de los DBMS ya usa la gramática SQL estándar.  
  
-   **ODBC proporciona un administrador de controladores para administrar el acceso simultáneo a varios de los DBMS.** Aunque el uso de controladores resuelve el problema de acceso simultáneamente a varios DBMS, el código para hacer esto puede ser complejo. Las aplicaciones que están diseñadas para funcionar con todos los controladores no se puede vincular estáticamente a todos los controladores. En su lugar, debe cargar los controladores en tiempo de ejecución y llamar a las funciones en ellos a través de una tabla de punteros de función. La situación es más compleja si la aplicación usa varios controladores al mismo tiempo.  
  
     En lugar de obligarle a cada aplicación para hacer esto, ODBC proporciona un administrador de controladores. El Administrador de controladores implementa todas las funciones ODBC - principalmente como acceso directo llamadas a funciones ODBC en los controladores - y estáticamente está vinculado a la aplicación o cargado por la aplicación en tiempo de ejecución. Por lo tanto, la aplicación llama a funciones ODBC por su nombre en el Administrador de controladores, en lugar de puntero en cada controlador.  
  
     Cuando una aplicación necesita un controlador determinado, primero solicita un identificador de conexión con la que se va a identificar el controlador y, a continuación, las solicitudes que el Administrador de controladores cargar el controlador. El Administrador de controladores se carga el controlador y se almacena la dirección de cada función en el controlador. Para llamar a una función ODBC en el controlador, la aplicación llama a esa función en el Administrador de controladores y pasa el identificador de conexión para el controlador. El Administrador de controladores, a continuación, llama a la función mediante la dirección almacenada anteriormente.  
  
-   **ODBC expone un número significativo de características de DBMS, pero no requieren controladores para admitir todas ellas.** Si ODBC expone solo las características que son comunes a todos los DBMS, puede resultar de poca utilidad; Después de todo, el motivo por lo que muchos DBMS diferentes existen hoy en día es que tienen características diferentes. Si ODBC expone todas las características que está disponible en cualquier sistema de DBMS, sería imposible para implementar los controladores.  
  
     En su lugar, ODBC expone un número significativo de características - algo más que son compatibles con la mayoría de los DBMS - pero requiere controladores para implementar solo un subconjunto de esas características. Controladores de implementan las características restantes solo si son compatibles con el DBMS subyacente o si deciden que emularlas. Por lo tanto, se pueden escribir aplicaciones para aprovechar las características DBMS único de forma expuesta por el controlador para ese DBMS, para usar solo las características usadas por todos los DBMS, o para comprobar la compatibilidad de una característica determinada y actuar en consecuencia.  
  
     Para que una aplicación puede determinar qué características de un controlador y admitir DBMS, ODBC proporciona dos funciones (**SQLGetInfo** y **SQLGetFunctions**) que devuelven información general sobre el controlador y el DBMS el controlador es compatible con capacidades y una lista de funciones. ODBC también define la API y SQL niveles de compatibilidad de gramática, que especifican intervalos amplios de las características admitidas por el controlador. Para obtener más información, consulte [niveles](../../odbc/reference/develop-app/conformance-levels.md).  
  
     Es importante recordar que ODBC define una interfaz común para todas las características que expone. Por este motivo, las aplicaciones contienen código específico de la característica, no código DBMS específicos y pueden usar los controladores que exponen estas características. Una ventaja de esto es que las aplicaciones no necesitan ser actualizadas cuando se han mejorado las características compatibles con un DBMS; en su lugar, cuando se instala un controlador actualizado, la aplicación utiliza automáticamente las características porque el código específico de la característica, no específicos del controlador o DBMS específicos.
