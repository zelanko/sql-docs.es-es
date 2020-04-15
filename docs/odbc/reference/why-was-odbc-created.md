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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22173b0ad3dd8abf2d168b41a16a03bc414022ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302786"
---
# <a name="why-was-odbc-created"></a>¿Por qué se creó ODBC?
Históricamente, las empresas utilizaban un único DBMS. Todo el acceso a la base de datos se realizaba a través del front-end de ese sistema o a través de aplicaciones escritas para trabajar exclusivamente con ese sistema. Sin embargo, a medida que el uso de computadoras creció y más hardware y software de computadoras se puso a disposición, las empresas comenzaron a adquirir diferentes DBMS. Las razones eran muchas: la gente compraba lo que era más barato, lo que era más rápido, lo que ya sabían, lo que era lo último en el mercado, lo que funcionaba mejor para una sola aplicación. Otras razones fueron las reorganizaciones y fusiones, donde los departamentos que antes tenían un solo DBMS ahora tenían varios.  
  
 El problema se hizo aún más complejo con la llegada de las computadoras personales. Estos equipos trajeron una serie de herramientas para consultar, analizar y mostrar datos, junto con una serie de bases de datos económicas y fáciles de usar. A partir de entonces, una sola corporación a menudo tenía datos dispersos en una miríada de escritorios, servidores y miniordenadores, almacenados en una variedad de bases de datos incompatibles, y a los que se accedía un gran número de herramientas diferentes, pocas de las cuales podían obtener en todos los datos.  
  
 El desafío final llegó con la llegada de la informática cliente/servidor, que busca hacer el uso más eficiente de los recursos informáticos. Las computadoras personales baratas (los clientes) se sentan en el escritorio y proporcionan un front-end gráfico a los datos y una serie de herramientas baratas, como hojas de cálculo, programas de gráficos y generadores de informes. Los miniordenadores y los ordenadores mainframe (los servidores) alojan los DBMS, donde pueden utilizar su potencia informática y su ubicación central para proporcionar un acceso rápido y coordinado a los datos. ¿Cómo se conectaba entonces el software front-end a las bases de datos back-end?  
  
 Un problema similar enfrentaba a proveedores de software independientes (ISV). Los proveedores que escribían software de base de datos para miniordenadores y mainframes generalmente se veían obligados a escribir una versión de una aplicación para cada DBMS o escribir código específico de DBMS para cada DBMS al que deseaban acceder. Los proveedores que escribían software para computadoras personales tenían que escribir rutinas de acceso a datos para cada DBMS diferente con el que querían trabajar. Esto a menudo significaba que una gran cantidad de recursos se gastaban en escribir y mantener rutinas de acceso a datos en lugar de aplicaciones, y las aplicaciones a menudo se vendían no en su calidad, sino en si podían acceder a los datos en un DBMS determinado.  
  
 Lo que ambos conjuntos de desarrolladores necesitaban era una forma de acceder a los datos en diferentes DBMS. El grupo de mainframe y miniordenador necesitaba una manera de combinar datos de diferentes DBMS en una sola aplicación, mientras que el grupo de computadoras personales necesitaba esta capacidad, así como una manera de escribir una sola aplicación que fuera independiente de cualquier DBMS. En resumen, ambos grupos necesitaban una forma interoperable de acceder a los datos; necesitaban conectividad de base de datos abierta.
