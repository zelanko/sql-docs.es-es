---
title: Cursores estáticos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 520c484bdaaa6eb59488900208993a607c5b0f7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924116"
---
# <a name="static-cursors"></a>Cursores estáticos
El cursor estático siempre muestra el conjunto de resultados tal como estaba al abrir el cursor por primera vez. En función de la implementación, los cursores estáticos son de solo lectura o de lectura/escritura y proporcionan un desplazamiento hacia delante y hacia atrás. Normalmente, el cursor estático no detecta los cambios realizados en la pertenencia, el orden o los valores del conjunto de resultados una vez abierto el cursor. Los cursores estáticos pueden detectar sus propias operaciones de inserción, actualización y eliminación, aunque no está obligados a hacerlo.  
  
 Los cursores estáticos nunca detectan otras actualizaciones, eliminaciones e inserciones. Por ejemplo, suponga que un cursor estático captura una fila y, después, otra aplicación la actualiza. Si la aplicación vuelve a capturar la fila del cursor estático, los valores que ve son iguales, a pesar de los cambios realizados por la otra aplicación. Se admiten todos los tipos de desplazamiento, pero los proveedores pueden admitir o no marcadores.  
  
 Si la aplicación no necesita detectar los cambios de datos y requiere desplazamiento, el cursor estático es la mejor opción. Use la variable **AdOpenStatic CursorTypeEnum** para indicar que desea utilizar un cursor estático en ADO.  
  
## <a name="see-also"></a>Consulte también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores de conjunto de claves](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
