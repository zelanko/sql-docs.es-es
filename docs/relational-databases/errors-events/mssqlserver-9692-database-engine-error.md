---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7041aa3e2262932541c4d81fe93dd1d9a740c97a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903814"
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9692|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SB2_CANT_LISTEN_PORT_IN_USE|  
|Texto del mensaje|El transporte de protocolo %S_MSG no puede escuchar en el puerto %d porque lo está utilizando otro proceso.|  
  
## <a name="explanation"></a>Explicación  
Otro programa del equipo está usando el puerto TCP indicado.  
  
## <a name="user-action"></a>Acción del usuario  
Ejecute **netstat -aon** para determinar qué programa está usando el puerto. Deshabilite esa aplicación o especifique otro puerto para Service Broker.  
  
