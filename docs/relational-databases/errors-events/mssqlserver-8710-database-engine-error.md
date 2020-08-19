---
description: MSSQLSERVER_8710
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4ba05822e61987454169064dfbc4ae54b0a74ef0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420909"
---
# <a name="mssqlserver_8710"></a>MSSQLSERVER_8710
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|MSSQLSERVER|  
|Id. de evento|8710|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Texto del mensaje|Las funciones de agregado que se utilizan con consultas CUBE, ROLLUP o GROUPING SET se deben proporcionar para la combinación de subagregados. Para solucionar este problema, quite la función de agregado o escriba la consulta utilizando UNION ALL en cláusulas GROUP BY.|  
  
## <a name="explanation"></a>Explicación  
Se ha usado una función de agregado con CUBE, ROLLUP o GROUPING SETS que no proporciona un método para combinar subagregados.  
  
## <a name="user-action"></a>Acción del usuario  
Para solucionar este problema, quite la función de agregado o escriba la consulta utilizando UNION ALL en cláusulas GROUP BY.  
  
