---
title: Transacciones ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da784f2af905aeeab914e4a2365978b1cdbec37c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="transactions-odbc"></a>Transacciones ODBC
A *transacciones* es una unidad de trabajo que se realiza como una única operación atómica; es decir, la operación se realiza correctamente o se produce un error como un todo. Por ejemplo, considere la posibilidad de transferir dinero de una cuenta bancaria a otra. Esto implica dos pasos: retirar el dinero de la primera cuenta y depositar en el segundo. Es importante que ambos pasos se realizan correctamente; no es aceptable para un solo paso, lleve a cabo correctamente y el otro no. Una base de datos que admite transacciones es capaz de garantizar esto.  
  
 Las transacciones pueden realizarse por va a *confirmada* o que se va a *revierte*. Cuando se confirma una transacción, los cambios realizados en que la transacción se hacen permanentes. Cuando se revierte una transacción, se devuelven las filas afectadas al estado que tenían antes de que se inició la transacción. Para ampliar el ejemplo de transferencia de la cuenta, una aplicación ejecuta una instrucción SQL para la primera cuenta de débito y una instrucción SQL diferente a la segunda cuenta de crédito. Si ambas instrucciones se realiza correctamente, la aplicación, a continuación, confirma la transacción. Pero si se produce un error en cualquier instrucción por cualquier motivo, la aplicación revierte la transacción. En cualquier caso, la aplicación garantiza un estado coherente al final de la transacción.  
  
 Una sola transacción puede estar formada por varias operaciones de base de datos que se producen en momentos diferentes. Si otras transacciones tenían acceso completo a los resultados intermedios, las transacciones pueden interferir con otros. Por ejemplo, imagine que una transacción inserta una fila, una segunda transacción lee esa fila y la primera transacción se revierte. La segunda transacción tiene datos de una fila que no existe.  
  
 Para solucionar este problema, hay varios esquemas para aislar las transacciones entre sí. *Aislamiento de transacción* generalmente se implementa por las filas de bloqueos, lo que impide más de una transacción del uso de la misma fila al mismo tiempo. En algunas bases de datos, el bloqueo de una fila también puede bloquear otras filas.  
  
 Transacción mayor aislamiento conlleva reducido *simultaneidad,* o la capacidad de dos transacciones para usar los mismos datos al mismo tiempo. Para obtener más información, consulte [establecer el nivel de aislamiento de transacción](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Transacciones en ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Aislamiento de transacción](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Control de simultaneidad](../../../odbc/reference/develop-app/concurrency-control.md)
