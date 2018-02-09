---
title: Los cursores KEYSET | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c59e2b203f6b33d94a1f615c53c2507964a13a65
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="keyset-cursors"></a>Cursores KEYSET
El cursor de conjunto de claves proporciona funcionalidad entre una variable static y un cursor dinámico en su capacidad para detectar los cambios. Al igual que un cursor estático, no siempre detecta cambios en la pertenencia y el orden del conjunto de resultados. Al igual que un cursor dinámico, detecta cambios en los valores de filas del conjunto de resultados.  
  
 Los cursores dinámicos se controlan mediante un conjunto de identificadores únicos (claves) que se conoce como el conjunto de claves. Las claves se generan a partir de un conjunto de columnas que identifican las filas del conjunto de resultados de forma unívoca. El conjunto de claves es el conjunto de valores de clave de todas las filas devueltas por la instrucción de consulta.  
  
 Con cursores dinámicos, se compila en una clave y guardan para cada fila del cursor y almacena en la estación de trabajo cliente o en el servidor. Cuando tiene acceso a cada fila, la clave almacenada se utiliza para capturar los valores de datos actuales del origen de datos. En un cursor controlado por conjunto de claves, la pertenencia a un conjunto de resultados está inmovilizada cuando se completa el conjunto de claves. A partir de ahí, adiciones o actualizaciones que afectan a la pertenencia no forman parte del conjunto de resultados hasta que se vuelva a abrir.  
  
 Cambios en los valores de datos (realizados por el propietario del conjunto de claves o por otros procesos) están visibles como el usuario se desplaza por el conjunto de resultados. Las inserciones realizadas fuera del cursor (por otros procesos) están visibles solo si el cursor se cierra y se vuelve a abrir. Las inserciones realizadas desde dentro del cursor están visibles al final del conjunto de resultados.  
  
 Cuando un cursor controlado por conjunto de claves intenta recuperar una fila que se ha eliminado, la fila aparece como un "agujero" en el conjunto de resultados. La clave para la fila existe en el conjunto de claves, pero la fila ya no existe en el conjunto de resultados. Si se actualizan los valores de clave en una fila, la fila se considera que se han eliminado y, a continuación, inserta, por lo que dichas filas también aparecen como agujeros en el conjunto de resultados. Mientras un cursor controlado por conjunto de claves siempre puede detectar filas eliminadas por otros procesos, si lo desea puede quitar las claves para las filas que elimina a sí mismo. Los cursores controlados por conjunto de claves que ello no pueden detectar sus propias eliminaciones porque se ha quitado la evidencia.  
  
 Una actualización a una columna de clave funciona como una eliminación de la clave antigua seguida de una instrucción insert de la nueva clave. El nuevo valor de clave no está visible si la actualización no se realizó a través del cursor. Si la actualización se realizó a través del cursor, el nuevo valor de clave es visible al final del conjunto de resultados.  
  
 Hay una variación en el nombre de cursores estándares cursores controlados por los cursores dinámicos. En un cursor estándar controlado por conjunto de claves, la pertenencia de filas del conjunto de resultados y el orden de las filas son fijos en el momento de apertura del cursor, aunque los cambios a los valores que se realizan por el propietario del cursor y los cambios confirmados realizados por otros procesos están visibles. Si un cambio descalifica a una fila para la pertenencia o afecta al orden de una fila, la fila no desaparecen o mover a menos que el cursor se cierra y se vuelve a abrir. Los datos insertados no aparecen, pero los cambios en los datos existentes aparecen tal y como se capturan las filas.  
  
 El cursor controlado por conjunto de claves es difícil de usar correctamente porque la sensibilidad a los cambios de datos depende de muchas circunstancias diferentes, como se describió anteriormente. Sin embargo, si la aplicación no está relacionada con las actualizaciones simultáneas, puede controlar mediante programación claves incorrectas y debe tener acceso directamente a ciertas filas con clave, el cursor controlado por conjunto de claves podría funcionar para usted. Utilice la **adOpenKeyset CursorTypeEnum** para indicar que desea utilizar un cursor de conjunto de claves en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
