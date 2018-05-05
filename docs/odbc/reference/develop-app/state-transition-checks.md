---
title: Comprobaciones de transición de estado | Documentos de Microsoft
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
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23f2b87fc943535075e1456bb31366ff9667b07b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="state-transition-checks"></a>Comprobaciones de transición de estado
El Administrador de controladores comprueba que el estado del entorno, la conexión o la instrucción es adecuado para la función que se llama. Por ejemplo, una conexión debe estar en una asignación estado cuando **SQLConnect** se denomina; debe ser una instrucción en un preparada estado cuando **SQLExecute** se llama. El Administrador de controladores devuelve SQL_ERROR si hay errores de transición de estado.
