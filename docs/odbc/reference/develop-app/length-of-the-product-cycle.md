---
description: Longitud del ciclo del producto
title: Duración del ciclo del producto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d1484079a09d10864e0563db95208e926a959d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476587"
---
# <a name="length-of-the-product-cycle"></a>Longitud del ciclo del producto
La última pregunta sobre la interoperabilidad es el tiempo. El desarrollo de una aplicación interoperable normalmente tarda más que desarrollar una noninteroperable. La razón es que la aplicación debe comprobar las capacidades de DBMS, realizar las mismas tareas de manera diferente para los distintos DBMS, resolver la funcionalidad admitida por algunos DBMS, pero no otros, etc.  
  
 Además del tiempo de desarrollo, se debe tener en cuenta la duración del producto. Si la aplicación está diseñada para usarse una vez, por ejemplo, una aplicación que transfiere datos al migrar de un DBMS a otro, no hay ningún punto para que sea interoperable. La aplicación se utilizará una vez y se descartará.  
  
 Si la aplicación va a existir durante mucho tiempo, podría ser más fácil de mantener como una aplicación interoperable. Esto es cierto incluso en el caso de las aplicaciones personalizadas que tienen un único DBMS como destino. La razón es que el código interoperable utiliza un subconjunto limitado de características de base de datos. El controlador es necesario para mantener esas características disponibles, incluso en caso de que se produzcan cambios en el DBMS subyacente. Por lo tanto, el código interoperable puede desplazar la carga de realizar cambios en el DBMS del desarrollador de aplicaciones al desarrollador de controladores.
