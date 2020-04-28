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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287879"
---
# <a name="manual-commit-mode"></a>Modo de confirmación manual
*En el modo de confirmación manual,* las aplicaciones deben completar explícitamente las transacciones mediante una llamada a **SQLEndTran** para confirmarlos o revertirlos. Este es el modo de transacción normal para la mayoría de las bases de datos relacionales.  
  
 No es necesario iniciar explícitamente las transacciones en ODBC. En su lugar, una transacción comienza implícitamente cada vez que la aplicación comienza a operar en la base de datos. Si el origen de datos requiere un inicio explícito de la transacción, el controlador debe proporcionarlo cada vez que la aplicación ejecuta una instrucción que requiere una transacción y no hay ninguna transacción actual.
