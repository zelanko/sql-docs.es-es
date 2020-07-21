---
title: Invocación de procedimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290776"
---
# <a name="procedure-invocation"></a>Invocación del procedimiento
Cuando se usa el controlador de Microsoft Access, los procedimientos se pueden invocar desde el controlador mediante la función **SQLExecDirect** o **SQLPrepare** con la sintaxis siguiente: {Call *procedure-Name* [(*parámetro*[,*parámetro*]...)]}. Tenga en cuenta que las expresiones no se admiten como parámetros de un procedimiento llamado.  
  
 Si un nombre de procedimiento incluye un guión, el nombre debe delimitarse con comillas dobles (').  
  
 Se puede llamar a una consulta con parámetros mediante la instrucción anterior.
