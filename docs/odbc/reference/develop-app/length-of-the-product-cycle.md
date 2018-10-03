---
title: Longitud del ciclo del producto | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c8a5b88f3fdca03be7740ba086e7ff61edbf684
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656153"
---
# <a name="length-of-the-product-cycle"></a>Longitud del ciclo del producto
La pregunta final sobre la interoperabilidad es el momento. Desarrollar una aplicación interoperable normalmente tarda más que desarrollar una noninteroperable. El motivo es que la aplicación debe comprobar las capacidades DBMS, realizar las mismas tareas de forma diferente para diferentes DBMS, solucionar funcionalidad admitida por algunos de los DBMS, pero no otros y así sucesivamente.  
  
 Además de tiempo de desarrollo, debe considerarse la vigencia del producto. Si la aplicación está diseñada para utilizarse una vez, por ejemplo, una aplicación que transfiere datos al migrar de un sistema DBMS a otro, no hay ningún punto en lo que interoperable. La aplicación se usa una vez y se descarta.  
  
 Si la aplicación existirá durante mucho tiempo, podría ser más fácil de mantener como una aplicación interoperable. Esto es verdad incluso para las aplicaciones personalizadas que tienen un único DBMS como destino. El motivo es que puede interoperar código usa un subconjunto limitado de características de base de datos. El controlador es necesario para mantener las características disponibles, aunque se produzcan cambios en el DBMS subyacente. Por lo tanto, interoperable código puede cambiar la carga de hacer frente a cambios a DBMS desde el desarrollador de aplicaciones para el programador del controlador.
