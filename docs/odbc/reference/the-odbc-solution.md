---
title: "La solución ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7288fcb9fad7b2567f7fec16cf0f407b2f6b2e4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="the-odbc-solution"></a>La solución ODBC
¿A continuación, la pregunta es cómo normalizar ODBC acceso de base de datos? Hay dos requisitos de arquitectura:  
  
-   Las aplicaciones deben poder tener acceso a varios DBMS usando el mismo código de origen sin volver a compilar o volver a vincular.  
  
-   Las aplicaciones deben poder tener acceso simultáneamente a varios de los DBMS.  
  
 Y no hay una pregunta más, debido a la realidad de marketplace:  
  
-   ¿Qué características DBMS debe exponer ODBC? ¿Solo las características que son comunes a todos los DBMS o todas las características que está disponible en cualquier DBMS?  
  
 ODBC soluciona estos problemas de la siguiente manera:  
  
-   **ODBC es una interfaz de nivel de llamada.** Para solucionar el problema de cómo las aplicaciones tener acceso a varios DBMS con el mismo código de origen, ODBC define una CLI estándar. Este contiene todas las funciones en las especificaciones de CLI de Open Group y ISO/IEC y proporciona funciones adicionales que normalmente requeridas por las aplicaciones.  
  
     Una biblioteca diferente, o el controlador, se requiere para cada DBMS que admita ODBC. El controlador implementa las funciones de la API de ODBC. Para usar un controlador diferente, la aplicación no necesita volver a compilar y vincular. En su lugar, la aplicación simplemente carga el controlador nuevo y llama a las funciones en ella. Para tener acceso simultáneamente a varios DBMS, la aplicación carga varios controladores. ¿Cómo se admiten los controladores es específicos del sistema operativo. Por ejemplo, en el sistema operativo Microsoft® Windows®, los controladores son bibliotecas de vínculos dinámicos (DLL).  
  
-   **ODBC define ninguna gramática SQL estándar.** Además de una interfaz de nivel de llamada estándar, ODBC define ninguna gramática SQL estándar. Esta gramática se basa en la especificación CAE de SQL de grupo abierto. Las diferencias entre las dos gramáticas son menores y principalmente debido a las diferencias entre la gramática SQL requerido embedded SQL (Open Group) y una CLI (ODBC). También hay algunas extensiones de la gramática de exponer las características de idioma disponibles normalmente no cubiertos por la gramática de Open Group.  
  
     Las aplicaciones pueden enviar las instrucciones que usan la gramática ODBC o específicos del DBMS. Si una instrucción utiliza la gramática ODBC que es diferente de gramática específica del DBMS, el controlador lo convierte antes de enviarlo al origen de datos. Sin embargo, estas conversiones son poco frecuentes, porque la mayoría de los DBMS ya utiliza la gramática SQL estándar.  
  
-   **ODBC proporciona un administrador de controladores para administrar el acceso simultáneo a varios de los DBMS.** Aunque el uso de controladores resuelve el problema de tener acceso simultáneamente a varios DBMS, el código para hacer esto puede ser complejo. Las aplicaciones que están diseñadas para trabajar con todos los controladores no se puede vincular estáticamente a todos los controladores. En su lugar, debe cargar controladores en tiempo de ejecución y llamar a las funciones en ellos a través de una tabla de punteros a función. La situación es más compleja si la aplicación usa varios controladores al mismo tiempo.  
  
     En lugar de obligarle a cada aplicación para hacer esto, ODBC proporciona un administrador de controladores. El Administrador de controladores implementa todas las funciones ODBC, principalmente como acceso directo llamadas a funciones ODBC en los controladores y estáticamente está vinculado a la aplicación o cargados por la aplicación en tiempo de ejecución. Por lo tanto, la aplicación llama a funciones ODBC por su nombre en el Administrador de controladores, en lugar de por el puntero en cada controlador.  
  
     Cuando una aplicación necesita un controlador específico, primero solicita un identificador de conexión con la que se va a identificar el controlador y, a continuación, las solicitudes que el Administrador de controladores cargar el controlador. El Administrador de controladores, se carga el controlador y almacena la dirección de cada función en el controlador. Para llamar a una función ODBC en el controlador, la aplicación llama a esa función en el Administrador de controladores y pasa el identificador de conexión para el controlador. El Administrador de controladores, a continuación, llama a la función mediante la dirección almacenada anteriormente.  
  
-   **ODBC expone un número significativo de características DBMS, pero no requieren controladores para admitir todas ellas.** Si ODBC expone solo las características que son comunes a todos los DBMS, sería de poco uso; Después de todo, la razón para que muchos DBMS diferentes en la actualidad existen es que tienen características diferentes. Si ODBC expone todas las características que está disponible en cualquier DBMS, sería imposible controladores implementar.  
  
     En su lugar, ODBC expone un número significativo de características, más que son compatibles con la mayoría de los DBMS, pero requiere controladores para implementar sólo un subconjunto de esas características. Controladores de implementan las características restantes solo si son compatibles con el DBMS subyacente o si así lo eligen emular a ellos. Por lo tanto, se pueden escribir aplicaciones para aprovechar las características de un DBMS único expuesto por el controlador para ese DBMS, para usar solo aquellas características que usan todos los DBMS, o para comprobar la compatibilidad de una característica determinada y actuar en consecuencia.  
  
     Para que una aplicación puede determinar qué características de un controlador y admitir DBMS, ODBC proporciona dos funciones (**SQLGetInfo** y **SQLGetFunctions**) que devuelven información general sobre el controlador y el DBMS el controlador es compatible con capacidades y una lista de funciones. ODBC también define API y SQL gramática niveles, que especifican intervalos amplios de las características admitidas por el controlador. Para obtener más información, consulte [niveles](../../odbc/reference/develop-app/conformance-levels.md).  
  
     Es importante recordar que ODBC define una interfaz común para todas las características que expone. Por este motivo, las aplicaciones contienen código específico de la característica, no el código de DBMS específico y pueden usar los controladores que exponen las características. Una ventaja de esto es que las aplicaciones no necesitan actualizarse cuando se han mejorado las características admitidas por un DBMS; en su lugar, cuando se instala un controlador actualizado, la aplicación utiliza automáticamente las características porque su código específico de la característica, no es específico del controlador o específicos del DBMS.
