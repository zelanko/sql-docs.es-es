---
title: Un nombre de canalización con nombre no válido puede bloquear la actualización | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094192"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Un nombre no válido de la canalización con nombre puede bloquear la actualización
  La actualización no es posible si el protocolo de canalizaciones con nombre no está configurado correctamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Durante la actualización, el programa de instalación [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] inicia la instancia con compatibilidad de memoria compartida, una canalización con nombre que solo acepta conexiones locales. Si el nombre de canalización especificado en el servidor no está en blanco, debe comenzar con la\\\\cadena\\".\pipe" para ser válido. Si el nombre de la canalización no es válido, [!INCLUDE[ssDE](../../includes/ssde-md.md)] no se iniciará y se producirá un error en la instalación.  
  
## <a name="corrective-action"></a>Acción correctora  
 Use la ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramienta de red** para proporcionar un nombre de canalización válido y, a continuación, ejecute el programa de instalación.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
