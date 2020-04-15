---
title: Duración del ciclo del producto ( Product Cycle) Microsoft Docs
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
ms.openlocfilehash: 3d235146ffe1b4699f0064c5772407bcf40ae962
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306198"
---
# <a name="length-of-the-product-cycle"></a>Longitud del ciclo del producto
La pregunta final sobre la interoperabilidad es el tiempo. El desarrollo de una aplicación interoperable suele tardar más que desarrollar una no interoperable. La razón es que la aplicación debe comprobar las capacidades de DBMS, realizar las mismas tareas de forma diferente para diferentes DBMS, evitar la funcionalidad admitida por algunos DBMS, pero no otros, etc.  
  
 Además del tiempo de desarrollo, se debe tener en cuenta la vida útil del producto. Si la aplicación está diseñada para usarse una vez, como una aplicación que transfiere datos al migrar de un DBMS a otro, no tiene sentido hacerlo interoperable. La aplicación se utilizará una vez y se descartará.  
  
 Si la aplicación existirá durante mucho tiempo, podría ser más fácil de mantener como una aplicación interoperable. Esto es cierto incluso para las aplicaciones personalizadas que tienen un único DBMS como destino. La razón es que el código interoperable utiliza un subconjunto limitado de características de base de datos. El controlador es necesario para mantener esas características disponibles, incluso ante los cambios en el DBMS subyacente. Por lo tanto, el código interoperable puede trasladar la carga de hacer frente a los cambios en el DBMS desde el desarrollador de aplicaciones al desarrollador del controlador.
