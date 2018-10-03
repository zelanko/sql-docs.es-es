---
title: Los cursores dinámicos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be6dc5a164220befb534368eace4f51f4dbd84e1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47719443"
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de claves
Un cursor dinámico se sitúa entre estático y un cursor dinámico en su capacidad para detectar los cambios. Al igual que un cursor estático, no siempre detecta los cambios realizados en la pertenencia y el orden del conjunto de resultados. Como un cursor dinámico, detecta cambios en los valores de las filas del conjunto de resultados (de acuerdo con el nivel de aislamiento de la transacción, según lo establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION).  
  
 Cuando se abre un cursor dinámico, guarda las claves para el conjunto de resultados completo; Esto corrige la aparente pertenencia y el orden del conjunto de resultados. A medida que el cursor se desplaza por el conjunto de resultados, utiliza las claves en este *keyset* para recuperar los valores de cada fila de datos actual. Por ejemplo, suponga que un cursor controlado por captura una fila y la otra aplicación, a continuación, actualiza esa fila. Si el cursor vuelve a obtener la fila, los valores que ve son los nuevos porque volver a capturar la fila con su clave. Por este motivo, los cursores controlados por siempre puede detectar los cambios realizados por sí mismos y otros.  
  
 Cuando el cursor se intenta recuperar una fila que se ha eliminado, esta fila aparece como un "agujero" en el conjunto de resultados: la clave para la fila existe en el conjunto de claves, pero la fila ya no existe en el conjunto de resultados. Si se actualizan los valores de clave en una fila, la fila se considera que se han eliminado y, a continuación, inserta, por lo que dichas filas también aparecen como agujeros en el conjunto de resultados. Mientras que un cursor dinámico siempre puede detectar las filas eliminadas por otros usuarios, puede quitar opcionalmente las claves para las filas elimina a sí mismo desde el conjunto de claves. Los cursores dinámicos que ello no pueden detectar sus propias eliminaciones. Si un cursor controlado por determinado detecta su propio eliminaciones se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.  
  
 Las filas insertadas por otros usuarios nunca son visibles para un cursor dinámico porque no hay claves de estas filas existen en el conjunto de claves. Sin embargo, un cursor dinámico, opcionalmente, puede agregar las claves para las filas se inserta en el conjunto de claves. Los cursores dinámicos que ello pueden detectar sus propias inserciones. Si un cursor controlado por determinado detecta su propio inserciones se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.  
  
 La matriz de Estados de fila especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para ninguna fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED, SQL_ROW_ADDED para las filas que se detecta como actualizados, elimina o inserta.  
  
 Los cursores dinámicos se implementan normalmente mediante la creación de una tabla temporal que contiene las claves para cada fila del conjunto de resultados. Dado que el cursor también debe determinar que si se han actualizado las filas, esta tabla también contiene una columna con información de control de versiones de fila.  
  
 Para desplazarse a través del conjunto de resultados original, el cursor dinámico abre un cursor estático a través de la tabla temporal. Para recuperar una fila en el conjunto de resultados original, el cursor primero recupera la clave adecuada en la tabla temporal y, a continuación, recupera los valores actuales de la fila. Si se utilizan cursores de bloque, el cursor debe recuperar varias claves y las filas.
