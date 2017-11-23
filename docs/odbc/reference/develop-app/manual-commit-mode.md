---
title: "Modo de confirmación manual | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3838b390c41dfab8010d728e1eab8bb5f410c67
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="manual-commit-mode"></a>Modo de confirmación manual
*En el modo de confirmación manual,* aplicaciones explícitamente deben completar las transacciones mediante una llamada a **SQLEndTran** confirmarlas o revertirlas. Éste es el modo de transacción normal para la mayoría de bases de datos relacionales.  
  
 Las transacciones en ODBC no es necesario que se inicie de forma explícita. En su lugar, una transacción se inicia implícitamente siempre que inicia la aplicación en funcionamiento en la base de datos. Si el origen de datos requiere inicio de transacciones explícitas, el controlador debe proporcionar cada vez que la aplicación ejecuta una instrucción que requiere una transacción y no hay ninguna transacción actual.
