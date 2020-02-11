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
ms.openlocfilehash: 8cfdd0babe84d309391b3e1ca546c4e05fdf1331
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049167"
---
# <a name="why-was-odbc-created"></a>¿Por qué se creó ODBC?
Históricamente, las empresas usaban un solo DBMS. Todo el acceso a la base de datos se realizó a través del front-end de ese sistema o a través de aplicaciones escritas para trabajar exclusivamente con ese sistema. Sin embargo, a medida que aumenta el uso de los equipos y más software y hardware, las empresas empezaron a adquirir DBMS diferentes. Los motivos fueron muchos: los usuarios compraron lo más económico, lo que era más rápido, lo que ya sabían, lo que era más reciente en el mercado, lo que mejor funcionó para una sola aplicación. Otras razones fueron las reorganizaciones y las fusiones, donde los departamentos que anteriormente tenían un solo DBMS ahora tenían varios.  
  
 El problema aumentó incluso más complejo con la llegada de los equipos personales. Estos equipos se incorporaron en un host de herramientas para consultar, analizar y Mostrar datos, junto con una serie de bases de datos económicas y fáciles de usar. A partir de ese momento, una sola Corporación a menudo tenía datos dispersos en una gran cantidad de equipos de escritorio, servidores y minicomputers, almacenados en una variedad de bases de datos incompatibles y a los que se accede mediante un gran número de herramientas diferentes, algunas de las cuales podrían obtenerse todos los datos.  
  
 El último desafío llegó con la llegada de la informática de cliente/servidor, que pretende hacer el uso más eficaz de los recursos del equipo. Los equipos personales (clientes) económicos se colocan en el escritorio y proporcionan un front-end gráfico a los datos y una serie de herramientas económicas, como hojas de cálculo, programas de gráficos y generadores de informes. Los equipos de Minicomputers y mainframe (los servidores) hospedan los DBMS, donde pueden usar su capacidad informática y su ubicación central para proporcionar acceso rápido y coordinado a los datos. ¿Cómo se ha conectado el software front-end a las bases de datos back-end?  
  
 Un problema similar surgido por fabricantes de software independientes (ISV). Los proveedores que escriben software de base de datos para minicomputers y mainframes solían tener que escribir una versión de una aplicación para cada DBMS o escribir código específico de DBMS para cada DBMS al que querían acceder. Los proveedores que escriben software para equipos personales tenían que escribir rutinas de acceso a datos para cada DBMS diferente con el que querían trabajar. A menudo, esto significaba una gran cantidad de recursos dedicados a escribir y mantener las rutinas de acceso a los datos en lugar de a las aplicaciones, y las aplicaciones a menudo se vendían no en su calidad, sino en si podían tener acceso a los datos de un DBMS determinado.  
  
 Lo que los dos conjuntos de desarrolladores necesitaba eran una manera de tener acceso a los datos de distintos DBMS. El grupo mainframe y minicomputer necesitaba una manera de combinar datos de distintos DBMS en una sola aplicación, mientras que el grupo de equipos personales necesitaba esta capacidad, así como una manera de escribir una sola aplicación que era independiente de un DBMS. En Resumen, ambos grupos necesitaba una manera interoperable de tener acceso a los datos; necesitaban abrir la conectividad de base de datos.
