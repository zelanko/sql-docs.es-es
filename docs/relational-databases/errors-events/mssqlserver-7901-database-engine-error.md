---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9d20c9fe7e2236485cde6edade7cbff778d6c3d4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780225"
---
# <a name="mssqlserver_7901"></a>MSSQLSERVER_7901
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|7901|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Texto del mensaje|Instrucción de reparación no procesada. No se permite este nivel de reparación cuando la base de datos está en modo de emergencia.|  
  
## <a name="explanation"></a>Explicación  
La base de datos está en modo de emergencia y se ha especificado un nivel de reparación distinto de REPAIR_ALLOW_DATA_LOSS. Las reparaciones no pueden llevarse a cabo en el modo de emergencia, a menos que se especifique REPAIR_ALLOW_DATA_LOSS.  
  
## <a name="user-action"></a>Acción del usuario  
Vuelva a ejecutar el comando y especifique la opción REPAIR_ALLOW_DATA_LOSS.  
  
