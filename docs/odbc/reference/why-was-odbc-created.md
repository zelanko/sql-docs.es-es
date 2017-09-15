---
title: "¿Por qué se creó ODBC? | Microsoft Docs"
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
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ab537128c572ef36bf4e0175f3bde1c8bedefc1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="why-was-odbc-created"></a>¿Por qué se creó ODBC?
Históricamente, las empresas usan un DBMS único. Todo el acceso de base de datos se realiza a través del front-end de dicho sistema o las aplicaciones escritas para trabajar exclusivamente con ese sistema. Sin embargo, como el uso de equipos que ha crecido y más hardware y software, empezó a estar disponibles, las empresas han comenzado a adquirir DBMS diferentes. Los motivos estaban muchos: personas comprado ¿cuál era más barato, ¿cuál era más rápido, lo que ya conocían, ¿cuál era más reciente en el mercado, lo que ha trabajado más de una sola aplicación. Otras razones eran reorganizaciones y fusiones, donde los departamentos que anteriormente tenían un DBMS único ahora tenían varios.  
  
 El problema que ha crecido más complejo con la llegada de los equipos personales. Estos equipos en el que se introducen en un host de herramientas para consultar, analizar y mostrar los datos, junto con un número de bases de datos económicos, fácil de usar. Desde ese momento, una única compañía a menudo tenía datos dispersos en una gran cantidad de equipos de sobremesa, servidores y microcomputadoras, almacena en una variedad de bases de datos incompatibles y obtener acceso a una gran cantidad de herramientas diferentes, algunos de los cuales se pudieron obtener en todos los datos.  
  
 El último reto suministrada con la llegada de cliente/servidor informática, que pretende hacer un uso más eficaz de los recursos del equipo. Equipos económicos (los clientes) se colocan en el escritorio y proporcionar tanto un front-end gráfico a los datos y un número de herramientas económicas, como hojas de cálculo, gráficos de programas y generadores de informes. Microcomputadoras y equipos del gran sistema (los servidores) hospedan el DBMS, donde puede usar su capacidad de proceso y la ubicación central para proporcionar acceso a datos rápida y coordinada. ¿Cómo fue el software de front-end se conecten a las bases de datos de back-end?  
  
 Un problema similar enfrenta los proveedores de software independientes (ISV). Los proveedores de software de base de datos para microcomputadoras y grandes sistemas de escritura normalmente se debe escribir una versión de una aplicación para cada DBMS o escribir código específico de DBMS para cada DBMS que deseaban tener acceso a. Los proveedores que escribir software para equipos personales se tenían que escribir rutinas de acceso a datos para cada DBMS diferente con el que deseaban trabajar. A menudo esto ha conllevado la enorme cantidad de recursos dedicados a escribir y mantener rutinas en lugar de las aplicaciones de acceso a datos y aplicaciones a menudo se vendieron no en su calidad sino también en pueden tener acceso a datos en un DBMS determinado.  
  
 Lo que necesita ambos conjuntos de desarrolladores era una manera para obtener acceso a datos en diferentes DBMS. El grupo de gran sistema y minicomputadoras necesitaba una manera para combinar datos de diferentes DBMS en una sola aplicación, mientras que el grupo de equipos personales necesita esta capacidad, así como una forma de escribir una sola aplicación que era independiente de cualquier un DBMS. En resumen, ambos grupos necesita una manera interoperable para tener acceso a datos; necesita abrir conectividad de base de datos.
