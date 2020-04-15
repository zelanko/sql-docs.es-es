---
title: Invocación de Procedimientos ( Procedure Invocation) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290776"
---
# <a name="procedure-invocation"></a>Invocación del procedimiento
Cuando se utiliza el controlador de Microsoft Access, se pueden invocar procedimientos desde el controlador mediante la función **SQLExecDirect** o **SQLPrepare** con la sintaxis siguiente: *nombre-procedimiento* de CALL [(*parámetro*[,*parámetro*]...).. Tenga en cuenta que las expresiones no se admiten como parámetros para un procedimiento llamado.  
  
 Si un nombre de procedimiento incluye un guión, el nombre debe delimitarse con comillas inversas (').  
  
 Se puede llamar a una consulta parametrizada mediante la instrucción anterior.
