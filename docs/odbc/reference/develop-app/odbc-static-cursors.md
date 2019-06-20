---
title: Los cursores estáticos ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ddd2b4d998ab2718757db4dd58de6aea8bee05e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62799008"
---
# <a name="odbc-static-cursors"></a>Cursores estáticos ODBC
Un cursor estático es una en la que el conjunto de resultados aparece como estática. Normalmente no detectar los cambios realizados en la pertenencia, orden o los valores del conjunto una vez abierto el cursor de resultados. Por ejemplo, suponga que un cursor estático recupera una fila y la otra aplicación, a continuación, actualiza esa fila. Si el cursor estático vuelve a obtener la fila, los valores que ve son iguales, a pesar de los cambios realizados por la otra aplicación.  
  
 Los cursores estáticos pueden detectar sus propias actualizaciones, eliminaciones e inserciones, aunque no tienen que hacerlo. Si un cursor estático determinado detectará estos cambios se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**. Los cursores estáticos detectan nunca otras actualizaciones, eliminaciones e inserciones.  
  
 La matriz de Estados de fila especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para ninguna fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED para filas actualizadas, elimina o inserta el cursor, suponiendo que el cursor puede detectar dichos cambios.  
  
 Los cursores estáticos son normalmente implementados mediante el bloqueo de las filas del conjunto de resultados o mediante la realización de una copia o de instantáneas, del resultado de establecer. Aunque el bloqueo de filas es relativamente fácil de hacer, tiene el inconveniente de reducir significativamente la simultaneidad. Realizar una copia permite mayor simultaneidad y permite que el cursor realizar un seguimiento de sus propias actualizaciones, eliminaciones y se inserta mediante la modificación de la copia. Sin embargo, una copia es más cara a realizar y puede desviarse de los datos subyacentes como que los datos se cambian por otros usuarios.
