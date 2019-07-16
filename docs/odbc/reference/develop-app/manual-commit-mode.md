---
title: Modo de confirmación manual | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7189a0586ba4f62091d5eb209a56931627bc6f7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036401"
---
# <a name="manual-commit-mode"></a>Modo de confirmación manual
*En el modo de confirmación manual,* aplicaciones explícitamente deben completar las transacciones mediante una llamada a **SQLEndTran** confirmarlas o revertirlas. Éste es el modo de transacción normal para la mayoría de bases de datos relacionales.  
  
 Transacciones en ODBC no es necesario que se inicie de forma explícita. En su lugar, una transacción comienza implícitamente cuando inicia la aplicación en funcionamiento en la base de datos. Si el origen de datos requiere inicio de transacciones explícitas, el controlador debe proporcionar cada vez que la aplicación ejecuta una instrucción que requiere una transacción y no hay ninguna transacción actual.
