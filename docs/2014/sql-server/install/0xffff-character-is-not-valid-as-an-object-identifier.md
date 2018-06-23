---
title: el carácter 0xFFFF no es válido como identificador de objeto | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ded2cd54bced9ae69e207a1b609688c2fcf3b633
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113504"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>El carácter 0xFFFF no es válido como identificador de objeto
  El Asesor de actualizaciones ha detectado el carácter 0xFFFF en un identificador de objeto. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, no se puede hacer referencia a objetos como bases de datos, tablas y columnas que contienen este carácter en su identificador, ni cambiarles el nombre si el modo de compatibilidad de bases de datos está establecido en 90 o posterior. Cuando actualice a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], las bases de datos de usuarios conservan su modo de compatibilidad. Antes de cambiar el modo de compatibilidad de bases de datos al 90 o posterior, cambie el nombre del objeto que contiene el carácter 0xFFFF.  
  
 Para obtener más información acerca de los identificadores, vea "Identificadores" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre los modos de compatibilidad de la base de datos, vea "sp_dbcmptlevel" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
