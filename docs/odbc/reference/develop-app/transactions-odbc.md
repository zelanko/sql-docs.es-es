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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6ce5decd2744c0ce9d753e355321a40d00fd620
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305812"
---
# <a name="transactions-odbc"></a>Transacciones ODBC
Un *transacciones* es una unidad de trabajo que se realiza como una única operación atómica; es decir, la operación se realiza correctamente o no como un todo. Por ejemplo, considere la posibilidad de transferir dinero de una cuenta bancaria a otra. Esto implica dos pasos: retirar el dinero de la primera cuenta y el depósito en el segundo. Es importante que ambos pasos se realizan correctamente; no es aceptable para un solo paso, lleve a cabo correctamente y el otro. Una base de datos que admite transacciones es capaz de garantizar esto.  
  
 Las transacciones pueden realizarse por siendo *confirmada* o que se va a *revierte*. Cuando se confirma una transacción, los cambios realizados en que la transacción se hacen permanentes. Cuando se revierte una transacción, se devuelven las filas afectadas al estado que se encontraban antes de que se inició la transacción. Para ampliar el ejemplo de transferencia de la cuenta, una aplicación ejecuta una instrucción SQL para la primera cuenta de débito y una instrucción SQL diferente a la segunda cuenta de crédito. Si ambas instrucciones se realice correctamente, a continuación, la aplicación confirma la transacción. Pero si se produce un error en cualquier instrucción por cualquier motivo, la aplicación revierte la transacción. En cualquier caso, la aplicación garantiza un estado coherente al final de la transacción.  
  
 Una única transacción puede abarcar varias operaciones de base de datos que se producen en momentos diferentes. Si otras transacciones tenían acceso completo a los resultados intermedios, las transacciones pueden interferir entre sí. Por ejemplo, supongamos que una transacción inserta una fila, una segunda transacción lee esa fila y la primera transacción se revierte. La segunda transacción tiene datos de una fila que no existe.  
  
 Para solucionar este problema, existen varios esquemas para aislar las transacciones entre sí. *Aislamiento de transacción* generalmente se implementa mediante el bloqueo de filas, lo que impide a más de una transacción del uso de la misma fila al mismo tiempo. En algunas bases de datos, el bloqueo de una fila también puede bloquear otras filas.  
  
 Transacciones mayor aislamiento conlleva reducido *simultaneidad,* o la capacidad de dos transacciones para usar los mismos datos al mismo tiempo. Para obtener más información, consulte [establecer el nivel de aislamiento de transacción](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Transacciones en ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Control de simultaneidad](../../../odbc/reference/develop-app/concurrency-control.md)
