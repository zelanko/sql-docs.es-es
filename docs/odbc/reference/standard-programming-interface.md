---
title: "Interfaz de programación estándar | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 235d61849f28b29af7ec0b9ba67fe86b38bf8239
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="standard-programming-interface"></a>Interfaz de programación estándar
La interfaz de programación es quizás la más obvio candidato para la estandarización. De hecho, cuando se estaba desarrollando ODBC, ANSI e ISO ya proporcionan estándares para embedded SQL y SQL módulos. Aunque no estándares existían para una base de datos CLI, el grupo de acceso de SQL: un consorcio de la industria de proveedores de base de datos, se considere la posibilidad de crear uno; partes de ODBC más adelante se convirtió en la base de su trabajo.  
  
 Uno de los requisitos para ODBC era que tenía una sola aplicación binaria trabajar con varios DBMS. Es por ello que ODBC no utiliza idiomas de módulo o SQL incrustados. Aunque el idioma en lenguajes SQL y módulo incrustados está normalizado, cada uno de ellos está asociado a precompilers específicos del DBMS. Por lo tanto, se deben volver a compilar aplicaciones para cada DBMS y los archivos binarios resultantes solo funcionan con un DBMS único. Aunque esto es aceptable para las aplicaciones de bajo volumen que se encuentra en los lenguajes minicomputadoras y mainframe, no es aceptable en el mundo de la informática personal. En primer lugar, es una pesadilla logística para ofrecer varias versiones de software de gran volumen, reducida a los clientes; en segundo lugar, las aplicaciones de PC a menudo necesitan tener acceso simultáneamente a varios de los DBMS.  
  
 Por otro lado, una interfaz de nivel de llamada puede implementarse a través de bibliotecas o controladores de base de datos, que residen en cada equipo local; tiene un controlador distinto para cada DBMS. Dado que los sistemas operativos modernos puede cargar estas bibliotecas (por ejemplo, bibliotecas de vínculos dinámicos en el sistema operativo Microsoft® Windows®) en tiempo de ejecución, una sola aplicación puede tener acceso a los datos de los DBMS tiene diferentes sin volver a compilar y también puede tener acceso a datos de varias bases de datos al mismo tiempo. Nuevos controladores de base de datos estén disponibles, los usuarios simplemente pueden instalar en sus equipos sin tener que modificar, volver a compilar o volver a vincular sus aplicaciones de base de datos. Además, una interfaz de nivel de llamada era un buen candidato para ODBC porque Windows: la plataforma para la que se desarrolló originalmente ODBC: ya realizados un amplio uso de estas bibliotecas.

