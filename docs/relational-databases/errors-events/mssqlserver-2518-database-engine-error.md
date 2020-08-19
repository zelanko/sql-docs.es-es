---
description: MSSQLSERVER_2518
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7cf4e144022aa76423f92d6250658c8a78c8926c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428767"
---
# <a name="mssqlserver_2518"></a>MSSQLSERVER_2518
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|2518|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|Texto del mensaje|Id. de objeto O_ID (objeto "O_NAME"): no es posible comprobar las columnas calculadas y los tipos definidos por el usuario para este objeto porque el entorno Common Language Runtime (CLR) está deshabilitado.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje informativo indica que el procesador de consultas no pudo proporcionar a DBCC un objeto interno para permitir la evaluación de las columnas calculadas y los tipos definidos por el usuario CLR (Common Language Runtime). Este problema se produjo porque una de las columnas utilizaba el CLR, pero éste no estaba habilitado. El objeto interno cubre todas las columnas. Por tanto, la imposibilidad de evaluar una sola columna evita que se cree el objeto interno. Esto significa que no se comprobará si las columnas calculadas son correctas o que no se usarán cuando DBCC compruebe la coherencia entre índices y tablas base.  
  
## <a name="user-action"></a>Acción del usuario  
Habilite el CLR y vuelva a ejecutar la instrucción DBCC.  
  
## <a name="see-also"></a>Consulte también  
[Habilitar la integración con CLR](~/relational-databases/clr-integration/clr-integration-enabling.md)  
  
