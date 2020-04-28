---
title: Cursores estáticos de ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282454"
---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Un cursor estático es aquél en el que el conjunto de resultados parece estático. Normalmente no detecta los cambios que se realizaron en la pertenencia, el orden o los valores del conjunto de resultados después de abrir el cursor. Por ejemplo, supongamos que un cursor estático captura una fila y otra aplicación actualiza esa fila. Si el cursor estático recupera la fila, los valores que ve no cambian, a pesar de los cambios realizados por la otra aplicación.  
  
 Los cursores estáticos pueden detectar sus propias actualizaciones, eliminaciones e inserciones, aunque no es necesario hacerlo. El hecho de que un cursor estático determinado detecte estos cambios se notifique a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**. Los cursores estáticos nunca detectan otras actualizaciones, eliminaciones e inserciones.  
  
 La matriz de estado de fila especificada por el atributo SQL_ATTR_ROW_STATUS_PTR instrucción puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para cualquier fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED para las filas actualizadas, eliminadas o insertadas por el cursor, suponiendo que el cursor puede detectar estos cambios.  
  
 Normalmente, los cursores estáticos se implementan bloqueando las filas del conjunto de resultados o realizando una copia, o instantánea, del conjunto de resultados. Aunque el bloqueo de filas es relativamente sencillo, tiene el inconveniente de reducir significativamente la simultaneidad. La realización de una copia permite una mayor simultaneidad y permite que el cursor realice un seguimiento de sus propias actualizaciones, eliminaciones e inserciones mediante la modificación de la copia. Sin embargo, una copia es más costosa de hacer y puede diferir de los datos subyacentes a medida que otros usuarios cambian los datos.
