---
title: Cursores de solo avance | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 121e8eec0b95f66b6e034f1f77d78c7d88fd5184
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="forward-only-cursors"></a>Cursores de solo avance
El tipo de cursor predeterminado típico, llamado a un cursor de solo avance (o no desplazable), sólo puede avanzar a través del conjunto de resultados. Un cursor de solo avance no admite el desplazamiento (la capacidad de mover hacia delante y hacia atrás en el conjunto de resultados); solo es compatible con la obtención de filas desde el principio hasta el final del conjunto de resultados. Con algunos cursores de solo avance (como con la biblioteca de cursores de SQL Server), todos los insert, update y las instrucciones delete realizadas por el usuario actual (o confirmados por otros usuarios) que afectan a las filas del conjunto de resultados son visibles cuando se capturan las filas. Dado que el cursor no se puede desplazar hacia atrás, sin embargo, los cambios realizados en las filas de la base de datos tras captura la fila no son visibles a través del cursor.  
  
 Después de procesan los datos de la fila actual, el cursor de sólo avance libera los recursos que se utilizan para almacenar esos datos. Cursores de solo avance son dinámicos de forma predeterminada, lo que significa que todos los cambios se detectan cuando se procesa la fila actual. Esto proporciona más rápida apertura del cursor y permite que el conjunto de resultados para mostrar las actualizaciones realizadas en las tablas subyacentes.  
  
 Mientras que los cursores de solo avance no admiten el desplazamiento hacia atrás, la aplicación puede volver al principio del conjunto de resultados por cerrar y volver a abrir el cursor. Se trata de una manera eficaz de trabajar con pequeñas cantidades de datos. Como alternativa, la aplicación puede leer el conjunto de resultados una vez, almacenar en caché los datos localmente y, a continuación, examinar la caché de datos local.  
  
 Si la aplicación no requiere desplazarse por el conjunto de resultados, el cursor de solo avance es la mejor manera de recuperar datos rápidamente con la menor cantidad de sobrecarga. Utilice la **adOpenForwardOnly CursorTypeEnum** para indicar que desea utilizar un cursor de sólo avance en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)

