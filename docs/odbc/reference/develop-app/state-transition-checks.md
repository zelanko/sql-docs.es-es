---
title: Comprobaciones de transición de estado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107283"
---
# <a name="state-transition-checks"></a>Comprobaciones de transición de estado
El administrador de controladores comprueba que el estado del entorno, la conexión o la instrucción es adecuado para la función a la que se llama. Por ejemplo, una conexión debe estar en un estado asignado cuando se llama a **SQLConnect** ; una instrucción debe estar en estado preparado cuando se llama a **SQLExecute** . El administrador de controladores devuelve SQL_ERROR para los errores de transición de estado.
