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
manager: craigg
ms.openlocfilehash: 1952d4185c80a3b49b7742a9dba1f3d8d41a6ca6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667923"
---
# <a name="manual-commit-mode"></a>Modo de confirmación manual
*En el modo de confirmación manual,* aplicaciones explícitamente deben completar las transacciones mediante una llamada a **SQLEndTran** confirmarlas o revertirlas. Éste es el modo de transacción normal para la mayoría de bases de datos relacionales.  
  
 Transacciones en ODBC no es necesario que se inicie de forma explícita. En su lugar, una transacción comienza implícitamente cuando inicia la aplicación en funcionamiento en la base de datos. Si el origen de datos requiere inicio de transacciones explícitas, el controlador debe proporcionar cada vez que la aplicación ejecuta una instrucción que requiere una transacción y no hay ninguna transacción actual.
