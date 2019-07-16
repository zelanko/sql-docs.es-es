---
title: Los cursores KEYSET | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c7a12d1579af407bca77c9fa61d660a84a09f04e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924906"
---
# <a name="keyset-cursors"></a>Cursores KEYSET
El cursor keyset proporciona la funcionalidad entre estático y un cursor dinámico en su capacidad para detectar los cambios. Al igual que un cursor estático, no siempre detecta los cambios realizados en la pertenencia y el orden del conjunto de resultados. Como un cursor dinámico, detecta cambios en los valores de las filas del conjunto de resultados.  
  
 Los cursores controlados por conjunto de claves se supervisan mediante un conjunto de identificadores únicos (claves) denominado conjunto de claves. Las claves se generan a partir de un conjunto de columnas que identifican las filas del conjunto de resultados de forma unívoca. El conjunto de claves es el conjunto de valores de clave de todas las filas devueltas por la instrucción de consulta.  
  
 Con los cursores controlados por conjunto de claves, se crea y se guarda una clave para cada fila del cursor y se almacena en la estación de trabajo cliente o en el servidor. Al acceder a cada fila, se usa la clave almacenada para capturar los valores de datos actuales desde el origen de datos. En un cursor controlado por conjunto de claves, la pertenencia al conjunto de resultados se inmoviliza cuando se completa totalmente el conjunto de claves. Por tanto, las adiciones o actualizaciones que afectan a la pertenencia no forman parte del conjunto de resultados hasta que se vuelva a abrir.  
  
 Cambios en los valores de datos (realizados por el propietario del conjunto de claves o por otros procesos) son visibles cuando el usuario se desplaza por el conjunto de resultados. Las operaciones de inserción realizadas fuera del cursor (por otros procesos) son visibles solo si el cursor se cierra y se vuelve a abrir. Las operaciones de inserción realizadas desde dentro del cursor son visibles al final del conjunto de resultados.  
  
 Cuando un cursor controlado por intenta recuperar una fila que se ha eliminado, la fila aparece como un "agujero" en el conjunto de resultados. La clave para la fila existe en el conjunto de claves, pero la fila ya no existe en el conjunto de resultados. Si se actualizan los valores de clave en una fila, la fila se considera que se han eliminado y, a continuación, inserta, por lo que dichas filas también aparecen como agujeros en el conjunto de resultados. Mientras que un cursor dinámico siempre puede detectar las filas eliminadas por otros procesos, opcionalmente pueden quitar las claves para las filas que elimina a sí mismo. Los cursores dinámicos que ello no pueden detectar sus propias eliminaciones porque se ha quitado la evidencia.  
  
 Una actualización de una columna de clave funciona como una eliminación de la clave antigua seguida de una inserción de la nueva clave. Nuevo valor de clave no está visible si no se realizó la actualización a través del cursor. Si se realizó la actualización a través del cursor, el nuevo valor de clave es visible al final del conjunto de resultados.  
  
 Hay una variación en los cursores dinámicos llamado controlado por cursores estándar. En un cursor estándar controlado por conjunto de claves, la pertenencia de las filas del conjunto de resultados y el orden de las filas son fijos en el momento de apertura del cursor, pero los cambios realizados en los valores que se realizan por el propietario del cursor y los cambios confirmados realizados por otros procesos están visibles. Si un cambio descalifica a una fila para la suscripción o afecta al orden de una fila, la fila no desaparecen o se mueva a menos que el cursor se cierra y vuelve a abrir. Los datos insertados no aparecen, pero los cambios realizados en los datos existentes tienen el aspecto que se recuperan las filas.  
  
 El cursor dinámico es difícil de usar correctamente porque la sensibilidad a los cambios de datos depende de muchas circunstancias diferentes, como se describió anteriormente. Sin embargo, si la aplicación no se ocupa de las actualizaciones simultáneas, puede controlar mediante programación claves incorrectas y debe tener acceso directamente a ciertas filas con clave, el cursor controlado por funcionen para usted. Utilice la **adOpenKeyset CursorTypeEnum** para indicar que desea utilizar un cursor keyset en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores dinámicos](../../../ado/guide/data/dynamic-cursors.md)
