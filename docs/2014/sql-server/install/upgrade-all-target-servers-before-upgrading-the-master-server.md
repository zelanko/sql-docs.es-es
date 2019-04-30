---
title: Actualice todos los servidores de destino antes de actualizar el servidor maestro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- TSX [SQL Server Agent]
- target servers [SQL Server Agent]
- MSX [SQL Server Agent]
- master servers [SQL Server Agent]
ms.assetid: 2c231793-3878-4a5e-a425-1fa0d787ba84
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97272209c1ceba780711ecf4a07178ddf8943d49
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156726"
---
# <a name="upgrade-all-target-servers-before-upgrading-the-master-server"></a>Actualizar todos los servidores de destino antes de actualizar el servidor maestro
  Antes de actualizar el servidor maestro, actualice todos los equipos que ejecuten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y estén configurados como servidores de destino.  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
## <a name="description"></a>Descripción  
 Para automatizar el proceso de administración en entornos con varios servidores, deberá disponer de al menos un servidor maestro y un servidor de destino. Los servidores maestros distribuyen trabajos a los servidores de destino y reciben eventos de éstos. Asimismo, almacenan la copia central de definiciones de trabajos ejecutados en servidores de destino.  
  
 Si el servidor actual se configura como un servidor maestro, actualice todos sus servidores de destino antes de actualizar el servidor maestro.  
  
## <a name="corrective-action"></a>Acción correctora  
 Si no puede actualizar todos los servidores de destino antes de actualizar el servidor maestro, debe dar de baja todos los servidores de destino y volverlos a dar de alta una vez haya llevado a cabo la actualización.  
  
 Para obtener más información, vea los temas "Automatizar la administración a través de una empresa", "Cómo: Dar de baja un servidor de destino desde un servidor maestro,"y" Cómo: Dar de alta un servidor de destino a un patrón" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)   
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
