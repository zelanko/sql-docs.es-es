---
title: La solución ODBC ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286758"
---
# <a name="the-odbc-solution"></a>La solución ODBC
La pregunta, entonces, es ¿cómo estandariza ODBC el acceso a la base de datos? Existen dos requisitos arquitectónicos:  
  
-   Las aplicaciones deben poder acceder a varios DBMS utilizando el mismo código fuente sin volver a compilar o volver a vincular.  
  
-   Las aplicaciones deben poder acceder a varios DBMS simultáneamente.  
  
 Y hay una pregunta más, debido a la realidad del mercado:  
  
-   ¿Qué características de DBMS debe exponer ODBC? ¿Solo las características que son comunes a todos los DBMS o cualquier característica que esté disponible en cualquier DBMS?  
  
 ODBC resuelve estos problemas de la siguiente manera:  
  
-   **ODBC es una interfaz de nivel de llamada.** Para resolver el problema de cómo las aplicaciones acceden a varios DBMS con el mismo código fuente, ODBC define una CLI estándar. Esto contiene todas las funciones en las especificaciones CLI de Open Group e ISO/IEC y proporciona funciones adicionales comúnmente requeridas por las aplicaciones.  
  
     Se requiere una biblioteca o controlador diferente para cada DBMS que admita ODBC. El controlador implementa las funciones en la API ODBC. Para utilizar un controlador diferente, no es necesario volver a compilar ni volver a vincular la aplicación. En su lugar, la aplicación simplemente carga el nuevo controlador y llama a las funciones en él. Para acceder a varios DBMS simultáneamente, la aplicación carga varios controladores. La forma en que se admiten los controladores es específica del sistema operativo. Por ejemplo, en el sistema operativo Microsoft® Windows®, los controladores son bibliotecas de vínculos dinámicos (DLL).  
  
-   **ODBC define una gramática SQL estándar.** Además de una interfaz de nivel de llamada estándar, ODBC define una gramática SQL estándar. Esta gramática se basa en la especificación CAE de SQL de grupo abierto. Las diferencias entre las dos gramáticas son menores y principalmente debido a las diferencias entre la gramática SQL requerida por SQL incrustado (Open Group) y una CLI (ODBC). También hay algunas extensiones a la gramática para exponer características de lenguaje comúnmente disponibles no cubiertas por la gramática de grupo abierto.  
  
     Las aplicaciones pueden enviar instrucciones mediante la gramática específica de ODBC o DBMS. Si una instrucción utiliza gramática ODBC que es diferente de la gramática específica de DBMS, el controlador la convierte antes de enviarla al origen de datos. Sin embargo, estas conversiones son raras porque la mayoría de los DBMS ya utilizan la gramática SQL estándar.  
  
-   **ODBC proporciona un Administrador de controladores para administrar el acceso simultáneo a varios DBMS.** Aunque el uso de controladores resuelve el problema de acceder a varios DBMS simultáneamente, el código para hacerlo puede ser complejo. Las aplicaciones diseñadas para trabajar con todos los controladores no se pueden vincular estáticamente a ningún controlador. En su lugar, deben cargar los controladores en tiempo de ejecución y llamar a las funciones en ellos a través de una tabla de punteros de función. La situación se vuelve más compleja si la aplicación utiliza varios controladores simultáneamente.  
  
     En lugar de forzar a cada aplicación a hacer esto, ODBC proporciona un Administrador de controladores. El Administrador de controladores implementa todas las funciones ODBC , principalmente como llamadas de paso a través de funciones ODBC en controladores, y está vinculado estáticamente a la aplicación o cargado por la aplicación en tiempo de ejecución. Por lo tanto, la aplicación llama a funciones ODBC por nombre en el Administrador de controladores, en lugar de por puntero en cada controlador.  
  
     Cuando una aplicación necesita un controlador determinado, primero solicita un identificador de conexión con el que identificar el controlador y, a continuación, solicita que el Administrador de controladores cargue el controlador. El Administrador de controladores carga el controlador y almacena la dirección de cada función en el controlador. Para llamar a una función ODBC en el controlador, la aplicación llama a esa función en el Administrador de controladores y pasa el identificador de conexión para el controlador. A continuación, el Administrador de controladores llama a la función mediante la dirección que almacenó anteriormente.  
  
-   **ODBC expone un número significativo de características de DBMS, pero no requiere controladores para admitir todas ellas.** Si ODBC expone solo las características que son comunes a todos los DBMS, sería de poca utilidad; después de todo, la razón por la que existen tantos DBMS diferentes hoy en día es que tienen diferentes características. Si ODBC expone todas las características que están disponibles en cualquier DBMS, sería imposible que los controladores se implementen.  
  
     En su lugar, ODBC expone un número significativo de características , más de las que admiten la mayoría de los DBMS, pero requiere que los controladores implementen solo un subconjunto de esas características. Los controladores implementan las características restantes solo si son compatibles con el DBMS subyacente o si deciden emularlas. Por lo tanto, las aplicaciones se pueden escribir para explotar las características de un único DBMS como expuesto por el controlador para ese DBMS, para utilizar sólo las características utilizadas por todos los DBMS, o para comprobar la compatibilidad de una característica determinada y reaccionar en consecuencia.  
  
     Para que una aplicación pueda determinar qué características admite un controlador y DBMS, ODBC proporciona dos funciones (**SQLGetInfo** y **SQLGetFunctions**) que devuelven información general sobre el controlador y las capacidades de DBMS y una lista de funciones que admite el controlador. ODBC también define los niveles de conformidad de la gramática de API y SQL, que especifican amplios rangos de características admitidas por el controlador. Para obtener más información, consulte Niveles de [conformidad](../../odbc/reference/develop-app/conformance-levels.md).  
  
     Es importante recordar que ODBC define una interfaz común para todas las características que expone. Debido a esto, las aplicaciones contienen código específico de la característica, no código específico de DBMS, y pueden usar cualquier controlador que exponga esas características. Una ventaja de esto es que las aplicaciones no necesitan actualizarse cuando se mejoran las características admitidas por un DBMS; en su lugar, cuando se instala un controlador actualizado, la aplicación utiliza automáticamente las características porque su código es específico de la característica, no específico del controlador o específico de DBMS.
