---
title: Quite las llamadas al comando DBCC CONCURRENCYVIOLATION desusado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
caps.latest.revision: 7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2486546efae7daa63441e12fa350ef878c7daa77
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261901"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>Quitar llamadas al comando desusado DBCC CONCURRENCYVIOLATION 
  El Asesor de actualizaciones ha detectado el uso del comando DBCC CONCURRENCYVIOLATION. Este comando ya no está disponible. Al ejecutar este comando, se devuelve el error 2526.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Ninguna versión reciente de la edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye un regulador de carga de trabajo; por ello, se ha quitado el comando.  
  
## <a name="corrective-action"></a>Acción correctora  
 Actualice las aplicaciones y los scripts para quitar todas las referencias a este comando desusado.  
  
## <a name="external-resources"></a>Recursos externos  
  
