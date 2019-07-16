---
title: Invocación del procedimiento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc37ef6d268dba71f8270909ea9c5b938ef3ee75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070493"
---
# <a name="procedure-invocation"></a>Invocación del procedimiento
Cuando se usa el controlador de Microsoft Access, los procedimientos se pueden invocar desde el controlador mediante la **SQLExecDirect** o **SQLPrepare** función con la sintaxis siguiente: {llamar *nombre del procedimiento*  [(*parámetro*[,*parámetro*]...)]}. Tenga en cuenta que no se admiten expresiones como parámetros a un procedimiento llamado.  
  
 Si un nombre de procedimiento incluye un guión, el nombre debe delimitarse con comillas atrás (').  
  
 Puede llamar a una consulta con parámetros mediante la instrucción anterior.
