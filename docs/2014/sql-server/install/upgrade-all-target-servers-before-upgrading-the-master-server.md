---
title: Actualice todos los servidores de destino antes de actualizar el servidor maestro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 2b6e08a384e20d64a7002171059db0d35dfd94a7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091473"
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
  
  
