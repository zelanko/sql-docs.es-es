---
title: Quitar llamadas al comando DBCC CONCURRENCYVIOLATION desusado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cde04ebfc2ea9996d1c9ed233123e5b66f6e81fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065204"
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
  
