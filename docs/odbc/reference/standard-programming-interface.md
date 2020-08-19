---
description: Interfaz de programación estándar
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fd0e9e3901ea6b3dcf9a09366b13fe532f1198
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448888"
---
# <a name="standard-programming-interface"></a>Interfaz de programación estándar
La interfaz de programación es quizás el candidato más obvio para la normalización. De hecho, cuando se desarrolló ODBC, ANSI e ISO ya ofrecían estándares para los módulos SQL y SQL incrustados. Aunque no existían estándares para una CLI de base de datos, el grupo de acceso de SQL, un consorcio del sector de proveedores de bases de datos, estaba considerando la posibilidad de crear uno; las partes de ODBC se convirtieron posteriormente en la base de su trabajo.  
  
 Uno de los requisitos para ODBC era que un único binario de aplicación tuviera que trabajar con varios DBMS. Por esta razón, ODBC no utiliza lenguajes SQL o de módulos incrustados. Aunque el lenguaje de los lenguajes incrustados de SQL y módulo está normalizado, cada uno está asociado a los precompiladores específicos de DBMS. Por lo tanto, las aplicaciones se deben volver a compilar para cada DBMS y los archivos binarios resultantes solo funcionan con un solo DBMS. Aunque esto es aceptable para las aplicaciones de bajo volumen que se encuentran en minicomputer y en los mundos de grandes sistemas, no es aceptable en el mundo de los equipos personales. En primer lugar, se trata de una pesadilla logística para ofrecer a los clientes varias versiones de software de gran volumen y contenido reducido. en segundo lugar, las aplicaciones de equipos personales suelen necesitar tener acceso a varios DBMS simultáneamente.  
  
 Por otro lado, una interfaz de nivel de llamada se puede implementar a través de bibliotecas, o controladores de base de datos, que residen en cada máquina local. se requiere un controlador diferente para cada DBMS. Dado que los sistemas operativos modernos pueden cargar dichas bibliotecas (por ejemplo, bibliotecas de vínculos dinámicos en el sistema operativo Microsoft® Windows®) en tiempo de ejecución, una sola aplicación puede tener acceso a los datos de distintos DBMS sin necesidad de volver a compilar y también puede tener acceso a los datos de varias bases de datos simultáneamente. A medida que los nuevos controladores de base de datos están disponibles, los usuarios solo pueden instalarlos en sus equipos sin tener que modificar, volver a compilar o volver a vincular sus aplicaciones de base de datos. Además, una interfaz de nivel de llamada era una buena candidata para ODBC porque Windows-la plataforma para la que se desarrolló ODBC originalmente (ya ha hecho un uso extensivo de dichas bibliotecas).
