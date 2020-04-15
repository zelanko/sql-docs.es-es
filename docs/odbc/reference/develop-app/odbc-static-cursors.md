---
title: Cursores estáticos ODBC (ODBC Static Cursors) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282454"
---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Un cursor estático es aquel en el que el conjunto de resultados parece ser estático. Normalmente no detecta los cambios realizados en la pertenencia, el orden o los valores del conjunto de resultados después de abrir el cursor. Por ejemplo, supongamos que un cursor estático recupera una fila y otra aplicación, a continuación, actualiza esa fila. Si el cursor estático recupera la fila, los valores que ve no se modifican, a pesar de los cambios realizados por la otra aplicación.  
  
 Los cursores estáticos pueden detectar sus propias actualizaciones, eliminaciones e inserciones, aunque no son necesarios para hacerlo. Si un cursor estático determinado detecta estos cambios se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**. Los cursores estáticos nunca detectan otras actualizaciones, eliminaciones e inserciones.  
  
 La matriz de estado de fila especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para cualquier fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED de las filas actualizadas, eliminadas o insertadas por el cursor, suponiendo que el cursor puede detectar dichos cambios.  
  
 Normalmente, los cursores estáticos se implementan bloqueando las filas del conjunto de resultados o realizando una copia o instantánea del conjunto de resultados. Aunque el bloqueo de filas es relativamente fácil de hacer, tiene el inconveniente de reducir significativamente la simultaneidad. La realización de una copia permite una mayor simultaneidad y permite al cursor realizar un seguimiento de sus propias actualizaciones, eliminaciones e inserciones modificando la copia. Sin embargo, una copia es más costosa de hacer y puede divergir de los datos subyacentes a medida que los datos son cambiados por otros.
