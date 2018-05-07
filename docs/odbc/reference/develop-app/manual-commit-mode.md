---
title: Modo de confirmación manual | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fde932df4d3eaa8e9ae3cceb2f28b6511dfb32d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="manual-commit-mode"></a>Modo de confirmación manual
*En el modo de confirmación manual,* aplicaciones explícitamente deben completar las transacciones mediante una llamada a **SQLEndTran** confirmarlas o revertirlas. Éste es el modo de transacción normal para la mayoría de bases de datos relacionales.  
  
 Las transacciones en ODBC no es necesario que se inicie de forma explícita. En su lugar, una transacción se inicia implícitamente siempre que inicia la aplicación en funcionamiento en la base de datos. Si el origen de datos requiere inicio de transacciones explícitas, el controlador debe proporcionar cada vez que la aplicación ejecuta una instrucción que requiere una transacción y no hay ninguna transacción actual.
