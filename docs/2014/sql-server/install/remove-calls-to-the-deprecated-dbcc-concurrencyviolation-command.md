---
title: Quitar llamadas al comando desusado DBCC CONCURRENCYVIOLATION | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a17b3c844afb6b8b804da258b0330d45dc7208e6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196864"
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
  