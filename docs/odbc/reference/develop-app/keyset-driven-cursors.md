---
title: Los cursores controlados por conjunto de claves | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eff91b12ebf378aa4bbcdbbfbdfa84c40a66f06b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de claves
Un cursor controlado por conjunto de claves está comprendida entre una variable static y un cursor dinámico en su capacidad para detectar los cambios. Al igual que un cursor estático, no siempre detecta cambios en la pertenencia y el orden del conjunto de resultados. Al igual que un cursor dinámico, que detectar cambios en los valores de filas del conjunto de resultados (de acuerdo con el nivel de aislamiento de la transacción, según lo establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION).  
  
 Cuando se abre un cursor controlado por conjunto de claves, guarda las claves para el conjunto de resultados completo; Esto corrige la aparente pertenencia y el orden del conjunto de resultados. Cuando el cursor se desplaza a través del conjunto de resultados, use las claves en esta *keyset* para recuperar los valores de datos actual para cada fila. Por ejemplo, suponga que un cursor controlado por conjunto de claves recupera una fila y otra aplicación, a continuación, actualiza esa fila. Si el cursor vuelve a obtener la fila, los valores que ve son los nuevos ya que volver a capturar la fila con la clave. Por este motivo, los cursores controlados por conjunto de claves siempre puede detectar los cambios realizados por sí mismos y otros usuarios.  
  
 Cuando el cursor se intenta recuperar una fila que se ha eliminado, esta fila aparece como un "agujero" en el conjunto de resultados: la clave para la fila existe en el conjunto de claves, pero la fila ya no existe en el conjunto de resultados. Si se actualizan los valores de clave en una fila, la fila se considera que se han eliminado y, a continuación, inserta, por lo que dichas filas también aparecen como agujeros en el conjunto de resultados. Mientras que un cursor controlado por conjunto de claves siempre puede detectar filas eliminadas por otros usuarios, puede quitar opcionalmente las claves para las filas elimina a sí mismo desde el conjunto de claves. Los cursores controlados por conjunto de claves que ello no pueden detectar sus propias eliminaciones. Si un cursor controlado por conjunto de claves determinado detecta sus propio eliminaciones se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.  
  
 Filas insertadas por otros usuarios nunca están visibles para un cursor controlado por conjunto de claves porque no hay claves para estas filas existen en el conjunto de claves. Sin embargo, un cursor controlado por conjunto de claves, opcionalmente, puede agregar las claves para las filas se inserta en el conjunto de claves. Los cursores controlados por conjunto de claves que ello pueden detectar sus propias inserciones. Si un cursor controlado por conjunto de claves determinado detecta sus propio inserciones se notifica a través de la opción SQL_STATIC_SENSITIVITY en **SQLGetInfo**.  
  
 La matriz de Estados de fila especificada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO o SQL_ROW_ERROR para ninguna fila. Devuelve SQL_ROW_UPDATED, SQL_ROW_DELETED o SQL_ROW_ADDED para las filas que detecta como actualizadas, eliminadas o insertadas.  
  
 Los cursores dinámicos se implementan normalmente mediante la creación de una tabla temporal que contiene las claves para cada fila del conjunto de resultados. Dado que el cursor también debe determinar que si se ha actualizado la fila, esta tabla también contiene una columna con la información de control de versiones de fila.  
  
 Para desplazarse por el conjunto de resultados original, el cursor controlado por conjunto de claves abre un cursor estático a través de la tabla temporal. Para recuperar una fila en el conjunto de resultados original, el cursor primero recupera la clave adecuada de la tabla temporal y, a continuación, recupera los valores actuales de la fila. Si se utilizan cursores de bloque, el cursor debe recuperar varias claves y filas.
