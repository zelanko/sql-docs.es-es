---
title: Tipos de cursores (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ead4e034fde49ac9826e63f091d7234ec0ecff7e
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272944"
---
# <a name="types-of-cursors-ado"></a>Tipos de cursores (ADO)
Como norma general, la aplicación debe utilizar el cursor más sencillo que proporciona el acceso a los datos necesarios. Cada característica de cursor adicional más allá de los conceptos básicos (solo avance, de sólo lectura, estático, con desplazamiento, sin búfer) tiene un precio: en la memoria de cliente, de carga de red o rendimiento. En muchos casos, las opciones de cursor predeterminado generan un cursor más complejo que realmente necesita la aplicación.  
  
 La elección del tipo de cursor depende de cómo la aplicación usa el conjunto de resultados y también en diversas consideraciones de diseño, incluido el tamaño del conjunto de resultados, porcentaje de los datos que se van a poder usar sensibilidad a los cambios de datos y rendimiento de la aplicación requisitos.  
  
 En lo más básico, la elección del cursor depende de si tiene que cambiar o simplemente ver los datos:  
  
-   Si solo tiene que desplazarse a través de un conjunto de resultados, pero sin cambiar los datos, use un [solo avance](../../../ado/guide/data/forward-only-cursors.md) o [estático](../../../ado/guide/data/static-cursors.md) cursor.  
  
-   Si tiene un conjunto de resultados grande y es necesario seleccionar unas pocas filas, use un [keyset](../../../ado/guide/data/keyset-cursors.md) cursor.  
  
-   Si desea sincronizar un conjunto de resultados con reciente agrega, cambia y elimina todos los usuarios simultáneos, utilice un [dinámica](../../../ado/guide/data/dynamic-cursors.md) cursor.  
  
 Aunque cada tipo de cursor parece distinto, tenga en cuenta que estos tipos de cursor no son tan variedades diferentes que simplemente el resultado de características y opciones superpuestas.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Cursores estáticos](../../../ado/guide/data/static-cursors.md)  
  
-   [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>Vea también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
