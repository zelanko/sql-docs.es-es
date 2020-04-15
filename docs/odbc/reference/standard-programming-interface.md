---
title: Interfaz de programación estándar (Standard Programming Interface) Microsoft Docs
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
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7767f113d0f70569ce253f0200cd35cb83915a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280001"
---
# <a name="standard-programming-interface"></a>Interfaz de programación estándar
La interfaz de programación es quizás el candidato más obvio para la estandarización. De hecho, cuando se estaba desarrollando ODBC, ANSI e ISO ya proporcionaban estándares para módulos SQL y SQL incrustados. Aunque no existían estándares para una CLI de base de datos, SQL Access Group, un consorcio de proveedores de bases de datos de la industria, estaba considerando si se debe crear uno; partes de ODBC más tarde se convirtió en la base de su trabajo.  
  
 Uno de los requisitos para ODBC era que un único binario de aplicación tenía que trabajar con varios DBMS. Es por esta razón que ODBC no utiliza SQL incrustado o lenguajes de módulo. Aunque el lenguaje en sql incrustado y los lenguajes de módulo está estandarizado, cada uno está vinculado a precompiladores específicos de DBMS. Por lo tanto, las aplicaciones deben volver a compilarse para cada DBMS y los archivos binarios resultantes solo funcionan con un único DBMS. Si bien esto es aceptable para las aplicaciones de bajo volumen que se encuentran en los mundos de miniordenador y mainframe, es inaceptable en el mundo de la computadora personal. En primer lugar, es una pesadilla logística entregar múltiples versiones de software de gran volumen, envuelto en contracción a los clientes; en segundo lugar, las aplicaciones informáticas personales a menudo necesitan acceder a varios DBMS simultáneamente.  
  
 Por otro lado, una interfaz de nivel de llamada se puede implementar a través de bibliotecas, o controladores de base de datos, que residen en cada equipo local; se requiere un controlador diferente para cada DBMS. Dado que los sistemas operativos modernos pueden cargar estas bibliotecas (como bibliotecas de vínculos dinámicos en el sistema operativo Microsoft® Windows®) en tiempo de ejecución, una sola aplicación puede tener acceso a datos de diferentes DBMS sin recompilación y también puede tener acceso a datos de varias bases de datos simultáneamente. A medida que los nuevos controladores de base de datos están disponibles, los usuarios pueden instalarlos en sus equipos sin tener que modificar, volver a compilar o volver a vincular sus aplicaciones de base de datos. Además, una interfaz de nivel de llamada era un buen candidato para ODBC porque Windows - la plataforma para la que se desarrolló originalmente ODBC - ya hizo un uso extensivo de estas bibliotecas.
