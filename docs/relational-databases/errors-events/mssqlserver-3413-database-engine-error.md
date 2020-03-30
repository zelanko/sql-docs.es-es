---
title: MSSQLSERVER_3413 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3413 (Database Engine error)
ms.assetid: 3fa07637-ba93-4633-aaf2-ade7d18bc487
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 84f983c9b450e625fdca08c46720a1cf22e8b84c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68098312"
---
# <a name="mssqlserver_3413"></a>MSSQLSERVER_3413
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3413|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|MARKDB|  
|Texto del mensaje|Id. de base de datos %d. No se pudo marcar la base de datos como sospechosa. Error del recorrido con Getnext NC en sys.databases.database_id. Consulte los errores anteriores del registro de errores para identificar la causa y corregir cualquier problema relacionado.|  
  
## <a name="explanation"></a>Explicación  
Se produjo un error inesperado al intentar marcar una base de datos de usuario como SUSPECT en el catálogo. El estado SUSPECT no será persistente.  
  
## <a name="user-action"></a>Acción del usuario  
Vea los errores anteriores y solucione el problema.  
  
