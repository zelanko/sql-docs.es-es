---
title: Nombre de la canalización con nombre no válido puede bloquear la actualización | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c94c1eeff18bff698e2a6353e29b72dd33278d03
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108029"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Un nombre no válido de la canalización con nombre puede bloquear la actualización
  La actualización no es posible si el protocolo de canalizaciones con nombre no está configurado correctamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Durante la actualización, el programa de instalación inicia el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instancia con compatibilidad con memoria compartida, una canalización con nombre que sólo acepta las conexiones locales. Si el nombre de canalización especificado en el servidor no está en blanco, debe comenzar con la cadena "\\\\. \pipe\\" sea válida. Si el nombre de la canalización no es válido, [!INCLUDE[ssDE](../../includes/ssde-md.md)] no se iniciará y se producirá un error en la instalación.  
  
## <a name="corrective-action"></a>Acción correctora  
 Use la  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] red utilidad** para proporcionar un nombre de canalización válido y, a continuación, ejecute el programa de instalación.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
