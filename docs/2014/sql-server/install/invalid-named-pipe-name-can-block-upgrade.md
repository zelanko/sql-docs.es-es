---
title: Nombre de la canalización con nombre no válido puede bloquear la actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dddd5da66f09226579a6366baa1a16a6ab00d6bf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094192"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Un nombre no válido de la canalización con nombre puede bloquear la actualización
  La actualización no es posible si el protocolo de canalizaciones con nombre no está configurado correctamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Durante la actualización, el programa de instalación se inicia el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instancia con la compatibilidad de memoria compartida, una canalización con nombre que solo acepta conexiones locales. Si el nombre de canalización especificado en el servidor no está en blanco, debe comenzar con la cadena "\\\\. \pipe\\" sea válido. Si el nombre de la canalización no es válido, [!INCLUDE[ssDE](../../includes/ssde-md.md)] no se iniciará y se producirá un error en la instalación.  
  
## <a name="corrective-action"></a>Acción correctora  
 Use la  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] red utilidad** para proporcionar un nombre de canalización válido y, a continuación, ejecute el programa de instalación.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
