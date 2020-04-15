---
title: Transacciones ODBC ( Transactions ODBC) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297960"
---
# <a name="transactions-odbc"></a>Transacciones ODBC
Una *transacción* es una unidad de trabajo que se realiza como una sola operación atómica; es decir, la operación se realiza correctamente o falla en su conjunto. Por ejemplo, considere la posibilidad de transferir dinero de una cuenta bancaria a otra. Esto implica dos pasos: retirar el dinero de la primera cuenta y depositarlo en la segunda. Es importante que ambos pasos tengan éxito; no es aceptable que un paso tenga éxito y el otro fracase. Una base de datos que admite transacciones puede garantizarlo.  
  
 Las transacciones se pueden completar *confirmando* o *revirtiendo.* Cuando se confirma una transacción, los cambios realizados en esa transacción se hacen permanentes. Cuando se revierte una transacción, las filas afectadas se devuelven al estado en el que se encontraban antes de que se iniciara la transacción. Para ampliar el ejemplo de transferencia de cuenta, una aplicación ejecuta una instrucción SQL para cargar la primera cuenta y una instrucción SQL diferente para abonar la segunda cuenta. Si ambas instrucciones se realizan correctamente, la aplicación confirma la transacción. Pero si se produce un error en alguna instrucción por cualquier motivo, la aplicación revierte la transacción. En cualquier caso, la aplicación garantiza un estado coherente al final de la transacción.  
  
 Una sola transacción puede abarcar varias operaciones de base de datos que se producen en momentos diferentes. Si otras transacciones tuvieran acceso completo a los resultados intermedios, las transacciones podrían interferir entre sí. Por ejemplo, supongamos que una transacción inserta una fila, una segunda transacción lee esa fila y se revierte la primera transacción. La segunda transacción ahora tiene datos para una fila que no existe.  
  
 Para resolver este problema, hay varios esquemas para aislar las transacciones entre sí. *El aislamiento* de transacciones generalmente se implementa bloqueando filas, lo que impide que más de una transacción use la misma fila al mismo tiempo. En algunas bases de datos, bloquear una fila también puede bloquear otras filas.  
  
 Con el aumento del aislamiento de transacciones se reduce la *simultaneidad o* la capacidad de dos transacciones para usar los mismos datos al mismo tiempo. Para obtener más información, consulte Establecer el nivel de aislamiento de [transacción](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Transacciones en ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Control de simultaneidad](../../../odbc/reference/develop-app/concurrency-control.md)
