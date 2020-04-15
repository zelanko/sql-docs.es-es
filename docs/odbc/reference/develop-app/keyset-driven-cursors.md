---
title: Cursores controlados por conjuntos de claves ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 814fca7d48f50aab51b6b4f7e34835be8c412e9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306210"
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de claves
Un cursor controlado por conjunto de claves se encuentra entre un cursor estático y un cursor dinámico en su capacidad para detectar cambios. Al igual que un cursor estático, no siempre detecta los cambios realizados en la pertenencia y el orden del conjunto de resultados. Al igual que un cursor dinámico, detecta cambios en los valores de las filas del conjunto de resultados (sujeto al nivel de aislamiento de la transacción, según lo establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION).  
  
 Cuando se abre un cursor controlado por conjunto de claves, guarda las teclas de todo el conjunto de resultados; esto corrige la pertenencia aparente y el orden del conjunto de resultados. A medida que el cursor se desplaza por el conjunto de resultados, utiliza las claves de este conjunto de *claves* para recuperar los valores de datos actuales para cada fila. Por ejemplo, supongamos que un cursor controlado por conjunto de claves recupera una fila y otra aplicación, a continuación, actualiza esa fila. Si el cursor recupera la fila, los valores que ve son los nuevos porque regraba la fila con su clave. Debido a esto, los cursores controlados por conjuntos de claves siempre detectan los cambios realizados por ellos mismos y otros.  
  
 Cuando el cursor intenta recuperar una fila que se ha eliminado, esta fila aparece como un "agujero" en el conjunto de resultados: la clave de la fila existe en el conjunto de claves, pero la fila ya no existe en el conjunto de resultados. Si se actualizan los valores de clave de una fila, se considera que la fila se ha eliminado y, a continuación, se ha insertado, por lo que dichas filas también aparecen como agujeros en el conjunto de resultados. Aunque un cursor controlado por conjunto de claves siempre puede detectar filas eliminadas por otros, opcionalmente puede quitar las claves de las filas que se elimina del conjunto de claves. Los cursores controlados por conjuntos de claves que lo hacen no pueden detectar sus propias eliminaciones. Si un cursor determinado controlado por conjunto de claves detecta sus propias eliminaciones se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.  
  
 Las filas insertadas por otros nunca son visibles para un cursor controlado por conjunto de claves porque no existen claves para estas filas en el conjunto de claves. Sin embargo, un cursor controlado por conjunto de claves puede agregar opcionalmente las claves de las filas que se inserta en el conjunto de claves. Los cursores controlados por conjuntos de claves que lo hacen pueden detectar sus propias inserciones. Si un cursor determinado controlado por conjunto de claves detecta sus propias inserciones se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.  
  
 La matriz de estado de fila especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para cualquier fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED de las filas que detecta como actualizadas, eliminadas o insertadas.  
  
 Los cursores controlados por conjuntos de claves se implementan normalmente mediante la creación de una tabla temporal que contiene las claves para cada fila del conjunto de resultados. Dado que el cursor también debe determinar si las filas se han actualizado, esta tabla también suele contener una columna con información de control de versiones de fila.  
  
 Para desplazarse por el conjunto de resultados original, el cursor controlado por conjunto de claves abre un cursor estático sobre la tabla temporal. Para recuperar una fila del conjunto de resultados original, el cursor recupera primero la clave adecuada de la tabla temporal y, a continuación, recupera los valores actuales de la fila. Si se utilizan cursores de bloque, el cursor debe recuperar varias claves y filas.
