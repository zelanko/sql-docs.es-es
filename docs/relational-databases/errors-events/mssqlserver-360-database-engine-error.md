---
title: MSSQLSERVER_360 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3ad12a38d7921ba2c10a4b044ca85035646db171
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723444"
---
# <a name="mssqlserver_360"></a>MSSQLSERVER_360
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|360|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DML_UPDATE_SPARSE_AND_COLSET|  
|Texto del mensaje|La lista de columnas de destino de una instrucción INSERT, UPDATE o MERGE no puede contener una columna dispersa y el conjunto de columnas que la contiene. Escriba de nuevo la instrucción para incluir la columna dispersa o el conjunto de columnas, pero no ambos.|  
  
## <a name="explanation"></a>Explicación  
Un conjunto de columnas es una representación XML sin tipo que combina algunas columnas de una tabla en una salida estructurada. Se ha intentado modificar tanto el conjunto de columnas como una columna incluida en dicho conjunto, produciendo dos referencias a la misma columna.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a escribir la instrucción para incluir referencias a la columna o al conjunto de columnas, pero no incluya ambos en la instrucción.  
  
