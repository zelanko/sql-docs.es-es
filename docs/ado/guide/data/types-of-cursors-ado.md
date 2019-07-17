---
title: Tipos de cursores (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00c89272d121898b6ac5af75022344acf1dceb28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923855"
---
# <a name="types-of-cursors-ado"></a>Tipos de cursores (ADO)
Como norma general, la aplicación debe usar el cursor más sencillo que proporciona acceso a los datos necesarios. Cada característica de cursor adicional más allá de los aspectos básicos (solo avance, de solo lectura, estáticos, desplazamiento, sin almacenamiento en búfer) tiene un precio, en la memoria del cliente, la carga de red o el rendimiento. En muchos casos, las opciones de cursor predeterminado generan un cursor más complejo que la aplicación realmente necesita.  
  
 La elección del tipo de cursor depende de cómo la aplicación usa el conjunto de resultados y también en varias consideraciones de diseño, incluido el tamaño del conjunto de resultados, el porcentaje de los datos que se utilizan probablemente, la sensibilidad a los cambios de datos y rendimiento de la aplicación requisitos.  
  
 En lo más básico, la elección del cursor depende de si tiene que cambiar o simplemente ver los datos:  
  
-   Si solo necesita desplazarse por un conjunto de resultados, pero no los datos modificados, utilice un [progresivo](../../../ado/guide/data/forward-only-cursors.md) o [estático](../../../ado/guide/data/static-cursors.md) cursor.  
  
-   Si tiene un conjunto de resultados grande y es necesario seleccionar unas pocas filas, use un [keyset](../../../ado/guide/data/keyset-cursors.md) cursor.  
  
-   Si desea sincronizar un conjunto de resultados con reciente agrega, cambia y elimina todos los usuarios simultáneos, utilice un [dinámica](../../../ado/guide/data/dynamic-cursors.md) cursor.  
  
 Aunque cada tipo de cursor parece distinto, tenga en cuenta que estos tipos de cursor no son tantas diferentes variedades como simple resultado de las características y opciones superpuestas.  
  
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
