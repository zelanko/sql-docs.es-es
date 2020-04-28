---
title: Cursores controlados por conjunto de claves | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306210"
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de claves
Un cursor controlado por conjunto de claves está entre un cursor estático y dinámico en su capacidad para detectar cambios. Al igual que un cursor estático, no siempre detecta los cambios realizados en la pertenencia y el orden del conjunto de resultados. Al igual que un cursor dinámico, detecta cambios en los valores de las filas del conjunto de resultados (de acuerdo con el nivel de aislamiento de la transacción, según establece el atributo de conexión SQL_ATTR_TXN_ISOLATION).  
  
 Cuando se abre un cursor controlado por conjunto de claves, se guardan las claves para todo el conjunto de resultados. Esto corrige la pertenencia aparente y el orden del conjunto de resultados. A medida que el cursor se desplaza por el conjunto de resultados, utiliza las claves de este *conjunto de claves* para recuperar los valores de datos actuales de cada fila. Por ejemplo, supongamos que un cursor controlado por conjunto de claves captura una fila y otra aplicación actualiza esa fila. Si el cursor recupera la fila, los valores que ve son los nuevos porque la fila se ha recuperado con su clave. Por este motivo, los cursores controlados por conjunto de claves siempre detectan los cambios realizados por sí mismos y otros.  
  
 Cuando el cursor intenta recuperar una fila que se ha eliminado, esta fila aparece como un "agujero" en el conjunto de resultados: la clave de la fila existe en el conjunto de claves, pero la fila ya no existe en el conjunto de resultados. Si se actualizan los valores de clave de una fila, se considera que la fila se ha eliminado y se ha insertado, por lo que dichas filas también aparecen como huecos en el conjunto de resultados. Aunque un cursor controlado por conjunto de claves siempre puede detectar filas eliminadas por otros, puede quitar opcionalmente las claves de las filas que se eliminan del conjunto de claves. Los cursores controlados por conjunto de claves que lo hacen no pueden detectar sus propias eliminaciones. El hecho de que un cursor controlado por conjunto de claves determinado detecte sus propias eliminaciones se envía a través de la opción SQL_STATIC_SENSITIVITY de **SQLGetInfo**.  
  
 Las filas insertadas por otras nunca están visibles para un cursor controlado por conjunto de claves porque no existen claves para estas filas en el conjunto de claves. Sin embargo, un cursor controlado por conjunto de claves puede agregar opcionalmente las claves para las filas que se insertan en el conjunto de claves. Los cursores controlados por conjunto de claves que lo hacen pueden detectar sus propias inserciones. El hecho de que un cursor controlado por conjunto de claves determinado detecte sus propias inserciones se notifique a través de la opción SQL_STATIC_SENSITIVITY de **SQLGetInfo**.  
  
 La matriz de estado de fila especificada por el atributo SQL_ATTR_ROW_STATUS_PTR instrucción puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para cualquier fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED para las filas que detecta como actualizadas, eliminadas o insertadas.  
  
 Normalmente, los cursores controlados por conjunto de claves se implementan mediante la creación de una tabla temporal que contiene las claves de cada fila del conjunto de resultados. Dado que el cursor también debe determinar si se han actualizado las filas, esta tabla también contiene normalmente una columna con información de versiones de fila.  
  
 Para desplazarse por el conjunto de resultados original, el cursor controlado por conjunto de claves abre un cursor estático en la tabla temporal. Para recuperar una fila en el conjunto de resultados original, el cursor recupera primero la clave adecuada de la tabla temporal y, a continuación, recupera los valores actuales de la fila. Si se usan cursores de bloque, el cursor debe recuperar varias claves y filas.
