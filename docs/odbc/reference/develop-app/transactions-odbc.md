---
title: Transacciones ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297960"
---
# <a name="transactions-odbc"></a>Transacciones ODBC
Una *transacción* es una unidad de trabajo que se realiza como una operación única y atómica. es decir, la operación se realiza correctamente o se produce un error en su conjunto. Por ejemplo, considere la posibilidad de transferir dinero de una cuenta bancaria a otra. Esto implica dos pasos: retirar el dinero de la primera cuenta y depositarlo en el segundo. Es importante que ambos pasos se realicen correctamente; no es aceptable que un paso se lleve a cabo correctamente y el otro para que se produzca un error. Una base de datos que admite transacciones es capaz de garantizar esto.  
  
 Las transacciones se pueden completar si se *confirman* o se *revierten*. Cuando se confirma una transacción, los cambios realizados en esa transacción se realizan de forma permanente. Cuando se revierte una transacción, las filas afectadas se devuelven al estado en que se encontraban antes de que se iniciara la transacción. Para extender el ejemplo de transferencia de cuenta, una aplicación ejecuta una instrucción SQL para adeudar la primera cuenta y una instrucción SQL diferente para abonar la segunda cuenta. Si ambas instrucciones se ejecutan correctamente, la aplicación confirma la transacción. Pero si se produce un error en cualquiera de las instrucciones por algún motivo, la aplicación revierte la transacción. En cualquier caso, la aplicación garantiza un estado coherente al final de la transacción.  
  
 Una sola transacción puede abarcar varias operaciones de base de datos que se producen en momentos diferentes. Si otras transacciones tenían acceso completo a los resultados intermedios, las transacciones podrían interferir entre sí. Por ejemplo, supongamos que una transacción inserta una fila, una segunda transacción Lee esa fila y la primera transacción se revierte. La segunda transacción tiene ahora datos para una fila que no existe.  
  
 Para solucionar este problema, hay varios esquemas para aislar las transacciones entre sí. Normalmente, el *aislamiento de transacciones* se implementa mediante el bloqueo de filas, lo que impide que más de una transacción utilice la misma fila al mismo tiempo. En algunas bases de datos, el bloqueo de una fila también puede bloquear otras filas.  
  
 Con un mayor aislamiento de transacción se reduce la *simultaneidad,* o la capacidad de dos transacciones de usar los mismos datos al mismo tiempo. Para obtener más información, vea [establecer el nivel de aislamiento de transacción](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Transacciones en ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Control de simultaneidad](../../../odbc/reference/develop-app/concurrency-control.md)
