---
title: Comprobaciones de la transición del estado (State Transition Checks) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299710"
---
# <a name="state-transition-checks"></a>Comprobaciones de transición de estado
El Administrador de controladores comprueba que el estado del entorno, la conexión o la instrucción es adecuado para la función a la que se llama. Por ejemplo, una conexión debe estar en un estado asignado cuando se llama a **SQLConnect;** una instrucción debe estar en un estado preparado cuando **sqlExecute** se llama. El Administrador de controladores devuelve SQL_ERROR para los errores de transición de estado.
