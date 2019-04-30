---
title: Interfaz de programación estándar | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e0e10a6b8c15b6522e6b34ab008295fc411fcd3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232061"
---
# <a name="standard-programming-interface"></a>Interfaz de programación estándar
La interfaz de programación es quizás el más evidente candidato para la estandarización. De hecho, al que se desarrolló ODBC, ANSI e ISO proporcionan estándares para embedded SQL y SQL módulos. Aunque no existían estándares para una base de datos, CLI, el grupo de acceso de SQL - un consorcio del sector de los proveedores de base de datos - se considere la posibilidad de crear uno; partes de ODBC más adelante se convirtió en la base de su trabajo.  
  
 Uno de los requisitos para ODBC fue que tenía una sola aplicación binaria trabajar con varios DBMS. Es por esta razón que ODBC no usa lenguajes SQL o módulo incrustados. Aunque el lenguaje en los idiomas SQL y el módulo incrustados está estandarizado, cada uno está asociado a precompilers específicos para DBMS. Por lo tanto, se deben volver a compilar aplicaciones para cada DBMS y los archivos binarios resultantes solo funcionan con un DBMS único. Aunque esto es aceptable para las aplicaciones de bajo volumen que se encuentra en el mundo minicomputadoras y mainframe, no es aceptable en el mundo de la informática personal. En primer lugar, es una pesadilla logística para ofrecer varias versiones de software de gran volumen, empaquetado a los clientes; en segundo lugar, las aplicaciones de PC suelen necesitar acceder simultáneamente a varios DBMS.  
  
 Por otro lado, se puede implementar una interfaz de nivel de llamada a través de bibliotecas o los controladores de base de datos, que residen en cada equipo local; Falta un controlador diferente para cada DBMS. Dado que los sistemas operativos modernos pueden cargar estas bibliotecas (por ejemplo, bibliotecas de vínculos dinámicos en el sistema operativo Microsoft® Windows®) en tiempo de ejecución, una sola aplicación puede tener acceso a datos de los DBMS tiene diferentes sin recompilación y también puede tener acceso a datos de varias bases de datos al mismo tiempo. Como los nuevos controladores de base de datos estén disponibles, los usuarios pueden simplemente instalar en sus equipos sin tener que modificar, volver a compilar o volver a vincular sus aplicaciones de base de datos. Además, una interfaz de nivel de llamada era un buen candidato para ODBC porque Windows - la plataforma para la que se desarrolló originalmente ODBC - ya ha realizado un amplio uso de estas bibliotecas.
