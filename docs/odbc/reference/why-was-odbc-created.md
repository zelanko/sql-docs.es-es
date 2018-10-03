---
title: ¿Por qué se creó ODBC? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: ba6eb993-316b-4650-bab8-d76583c00e53
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 871919554975f04fae0aeaa1b8e6ec684c6650a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729303"
---
# <a name="why-was-odbc-created"></a>¿Por qué se creó ODBC?
Históricamente, las empresas usan un DBMS único. Todo el acceso de base de datos se realiza a través de la parte frontal de dicho sistema o las aplicaciones escritas para trabajar exclusivamente con ese sistema. Sin embargo, como el uso de los equipos que ha crecido y más software y hardware del equipo empezó a estar disponibles, las empresas se ha iniciado adquirir diferentes DBMS. Las razones por las que estaban muchas: personas compradas a lo que era más barato, lo que más rápida, lo que ya sabían, ¿cuál era más reciente en el mercado, lo que ha funcionado mejor para una sola aplicación. Otros motivos eran reorganizaciones y fusiones, donde los departamentos que anteriormente tenían un DBMS único ahora tenían varios.  
  
 El problema que ha crecido incluso más complejo con la llegada de los equipos personales. Estos equipos han aportado una gran cantidad de herramientas para consultar, analizar y mostrar los datos, junto con un número de bases de datos económicas, fácil de usar. Desde ese momento, una empresa única a menudo tenía datos distribuidos en un gran número de equipos de escritorio, servidores y miniequipos, almacenados en una variedad de bases de datos incompatibles y accediendo a un gran número de herramientas diferentes, algunos de los cuales se podrían obtener en todos los datos.  
  
 El último reto suministrada con la llegada de informática de cliente/servidor que pretende hacer el uso más eficaz de los recursos del equipo. Equipos económicos (los clientes) se colocan en el escritorio y proporcionar ambos un front-end gráfico para los datos y un número de herramientas económicas, como hojas de cálculo, programas y generadores de informes de gráficos. Miniequipos y equipos de gran sistema (servidores) hospedan el DBMS, donde puede usar su capacidad de proceso y la ubicación central para proporcionar acceso a datos rápido y coordinada. ¿Fue cómo, a continuación, el software de front-end se conecten a las bases de datos de back-end?  
  
 Un problema similar que enfrenta los proveedores de software independientes (ISV). Los proveedores de software de base de datos para miniequipos y grandes sistemas de escritura normalmente se veían obligados a escribir una versión de una aplicación para cada DBMS o escribir código específico de DBMS para cada DBMS que querían obtener acceso a. Los proveedores de escribir software para equipos personales tenían que escribir rutinas de acceso a datos para cada diferentes DBMS que deseaban trabajar. Esto significaba a menudo una gran cantidad de recursos dedicados a escribir y mantener las rutinas en lugar de las aplicaciones de acceso a datos y aplicaciones a menudo se vendieron no en su calidad, pero en la podrían tener acceso a datos en un sistema DBMS.  
  
 Lo que necesita ambos conjuntos de desarrolladores era una manera de acceder a los datos en diferentes DBMS. El grupo de mainframe y minicomputadoras necesitaba una manera de combinar datos de diferentes DBMS en una sola aplicación, mientras que el grupo de equipos personales necesita esta capacidad, así como una manera de escribir una única aplicación que era independiente de cualquier un DBMS. En resumen, ambos grupos necesita una manera interoperable para tener acceso a datos; es necesario que abran la conectividad de base de datos.
