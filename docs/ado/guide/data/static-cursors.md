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
manager: craigg
ms.openlocfilehash: e8815522ee4f9a4221887696a23a201910d7cfad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654193"
---
# <a name="static-cursors"></a>Cursores estáticos
El cursor estático siempre muestra el resultado que establece que tenía cuando el cursor se abre por primera vez. Según la implementación, los cursores estáticos pueden ser de solo lectura o lectura/escritura y proporcionar desplazamiento hacia delante y hacia atrás. El cursor estático normalmente no detecta los cambios realizados en la pertenencia, orden o los valores del conjunto una vez abierto el cursor de resultados. Cursores estáticos pueden detectar sus propias actualizaciones, eliminaciones e inserciones, aunque no tienen que hacerlo.  
  
 Los cursores estáticos detectan nunca otras actualizaciones, eliminaciones e inserciones. Por ejemplo, suponga que un cursor estático recupera una fila y la otra aplicación, a continuación, actualiza esa fila. Si la aplicación vuelve a obtener la fila del cursor estático, los valores que ve son iguales, a pesar de los cambios realizados por la otra aplicación. Se admiten todos los tipos de desplazamiento, pero los proveedores pueden o no admitir marcadores.  
  
 Si no necesita la aplicación detectar datos cambia y requiere que el desplazamiento, el cursor estático es la mejor opción. Utilice la **adOpenStatic CursorTypeEnum** para indicar que desea utilizar un cursor estático en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
