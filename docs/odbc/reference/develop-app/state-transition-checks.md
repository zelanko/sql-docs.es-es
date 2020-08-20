---
description: Comprobaciones de transición de estado
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50a845f2b83ada7c9d4f03f252b6d2bc3d3eff3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476377"
---
# <a name="state-transition-checks"></a>Comprobaciones de transición de estado
El administrador de controladores comprueba que el estado del entorno, la conexión o la instrucción es adecuado para la función a la que se llama. Por ejemplo, una conexión debe estar en un estado asignado cuando se llama a **SQLConnect** ; una instrucción debe estar en estado preparado cuando se llama a **SQLExecute** . El administrador de controladores devuelve SQL_ERROR para los errores de transición de estado.
