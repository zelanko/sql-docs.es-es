---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b099b983579c9a22f4105711f886c5512c1d139
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618323"
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1807|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|CANNOT_EX_LOCK|  
|Texto del mensaje|No se puede obtener un bloqueo exclusivo en la base de datos '%.*ls'. Intente la operación en otro momento.|  
  
## <a name="explanation"></a>Explicación  
Una operación que necesita acceso exclusivo a la base de datos no pudo obtenerlo.  
  
## <a name="user-action"></a>Acción del usuario  
Desconecte todas las conexiones a esa base de datos o vuelva a intentar ejecutar la consulta en otro momento.  
  
