---
title: Cursores de solo avance | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 15d11b8882e8e39a03ffb7509526a4f66b6553b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700703"
---
# <a name="forward-only-cursors"></a>Cursores de solo avance
El tipo de cursor predeterminado típico, llama a un cursor de solo avance (o no desplazable), sólo puede avanzar por el conjunto de resultados. Un cursor de solo avance no admite el desplazamiento (la capacidad de desplazarse hacia delante y hacia atrás en el conjunto de resultados); solo admite captura las filas desde el principio hasta el final del conjunto de resultados. Con algunos cursores de solo avance (como con la biblioteca de cursores de SQL Server), todos los insert, update y las instrucciones delete realizadas por el usuario actual (o confirmados por otros usuarios) que afectan a las filas del conjunto de resultados son visibles cuando se recuperan las filas. Pero como el cursor no se puede desplazar hacia atrás, los cambios realizados en las filas de la base de datos tras capturar la fila no son visibles a través del cursor.  
  
 Después de procesan los datos de la fila actual, el cursor de solo avance libera los recursos que se usaron para contener los datos. Los cursores de solo avance son dinámicos de forma predeterminada, lo que significa que todos los cambios se detectan cuando se procesa la fila actual. Esto proporciona una apertura del cursor más rápida y permite que el conjunto de resultados muestre las actualizaciones realizadas en las tablas subyacentes.  
  
 Mientras que los cursores de solo avance no admiten el desplazamiento hacia atrás, la aplicación podrá volver al principio del conjunto de resultados por cerrar y volver a abrir el cursor. Se trata de una forma eficaz de trabajar con pequeñas cantidades de datos. Como alternativa, la aplicación podría leer el conjunto de resultados una vez, almacenar en caché los datos localmente y, a continuación, examinar la caché de datos local.  
  
 Si la aplicación no requiere desplazarse por el conjunto de resultados, el cursor de solo avance es la mejor manera de recuperar los datos rápidamente con la menor cantidad de sobrecarga. Utilice la **adOpenForwardOnly CursorTypeEnum** para indicar que desea utilizar un cursor de solo avance en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
