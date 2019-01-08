---
title: ¿Qué es un bloqueo? | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 744ae9a9541b5c73d579e097f375b4141e771fce
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501759"
---
# <a name="what-is-a-lock"></a>¿Qué es un bloqueo?
El bloqueo es el proceso mediante el cual un DBMS restringe el acceso a una fila en un entorno multiusuario. Cuando está bloqueado exclusivamente una fila o columna, no se permiten otros usuarios para tener acceso a los datos bloqueados hasta que se libere el bloqueo. Esto garantiza que dos usuarios no puedan actualizar simultáneamente la misma columna en una fila.  
  
 Los bloqueos pueden ser muy costosos desde una perspectiva de los recursos y deben usarse solo cuando sea necesario para mantener la integridad de datos. En una base de datos donde cientos o miles de usuarios podrían estar intentando tener acceso a un registro cada segundo: por ejemplo, una base de datos conectado a Internet, el bloqueo innecesario rápidamente podría provocar un rendimiento más lento en la aplicación.  
  
 Puede controlar cómo el origen de datos y la biblioteca de cursores ADO administran la simultaneidad eligiendo la opción de bloqueo apropiada.  
  
 Establecer el **LockType** propiedad antes de abrir un **Recordset** para especificar qué tipo de bloqueo que el proveedor debe usar al abrirlo. Leer la propiedad para devolver el tipo de bloqueo en uso en una página abierta **Recordset** objeto.  
  
 Los proveedores podrían no admitir todos los tipos de bloqueo. Si un proveedor no admite solicitado **LockType** establecer, sustituirá por otro tipo de bloqueo. Para determinar la funcionalidad de bloqueo real disponible en un **Recordset** de objeto, utilice el [admite](../../../ado/reference/ado-api/supports-method.md) método con **adUpdate** y **adUpdateBatch**.  
  
 El **adLockPessimistic** configuración no se admite si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient.** Si se establece un valor no admitido, se producirá ningún error; admite la más cercana **LockType** se usará en su lugar.  
  
 El **LockType** propiedad es de lectura/escritura cuando el **Recordset** está cerrado y solo lectura cuando se abre.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de bloqueos](../../../ado/guide/data/types-of-locks.md)
