---
title: Los cursores estáticos | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924116"
---
# <a name="static-cursors"></a>Cursores estáticos
El cursor estático siempre muestra el resultado que establece que tenía cuando el cursor se abre por primera vez. Según la implementación, los cursores estáticos pueden ser de solo lectura o lectura/escritura y proporcionar desplazamiento hacia delante y hacia atrás. El cursor estático normalmente no detecta los cambios realizados en la pertenencia, orden o los valores del conjunto una vez abierto el cursor de resultados. Los cursores estáticos pueden detectar sus propias operaciones de inserción, actualización y eliminación, aunque no está obligados a hacerlo.  
  
 Los cursores estáticos detectan nunca otras actualizaciones, eliminaciones e inserciones. Por ejemplo, suponga que un cursor estático captura una fila y, después, otra aplicación la actualiza. Si la aplicación vuelve a capturar la fila del cursor estático, los valores que ve son iguales, a pesar de los cambios realizados por la otra aplicación. Se admiten todos los tipos de desplazamiento, pero los proveedores pueden o no admitir marcadores.  
  
 Si no necesita la aplicación detectar datos cambia y requiere que el desplazamiento, el cursor estático es la mejor opción. Utilice la **adOpenStatic CursorTypeEnum** para indicar que desea utilizar un cursor estático en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
