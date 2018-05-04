---
title: Longitud del ciclo del producto | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a0f319b92afac55101bfe3bca9766a53a91744d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-the-product-cycle"></a>Longitud del ciclo del producto
La pregunta final acerca de la interoperabilidad es el tiempo. Desarrollar una aplicación interoperable normalmente tarda más que desarrollar una noninteroperable. La razón es que la aplicación debe comprobar las capacidades DBMS, realizar las mismas tareas de forma diferente para distintos DBMS, solucionar funcionalidad admitida por algunos de los DBMS, pero no en otros y así sucesivamente.  
  
 Además de tiempo de desarrollo, debe considerarse la vigencia del producto. Si la aplicación está diseñada para utilizarse una vez, por ejemplo, una aplicación que transfiere datos al migrar desde un sistema DBMS a otro, no hay ningún punto en lo que interoperable. La aplicación se usa una vez y se descartan.  
  
 Si la aplicación existirá durante mucho tiempo, puede que sea más fácil de mantener como una aplicación interoperable. Esto es verdad incluso para las aplicaciones personalizadas que tienen un DBMS único como un destino. La razón es que el código interoperable utiliza un subconjunto limitado de funciones de base de datos. El controlador es necesario para mantener las características disponibles, incluso aunque se modifiquen el DBMS subyacente. Por lo tanto, interoperable código puede cambiar la carga de hacer frente a cambios en el DBMS de desarrollador de la aplicación para el programador del controlador.
