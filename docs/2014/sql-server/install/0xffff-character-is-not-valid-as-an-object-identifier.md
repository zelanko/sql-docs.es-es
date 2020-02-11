---
title: el carácter 0xFFFF no es válido como identificador de objeto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35c7c65bc312cd20c057b5e2603e7a8f77ce8c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096919"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>El carácter 0xFFFF no es válido como identificador de objeto
  El Asesor de actualizaciones ha detectado el carácter 0xFFFF en un identificador de objeto. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, no se puede hacer referencia a objetos como bases de datos, tablas y columnas que contienen este carácter en su identificador, ni cambiarles el nombre si el modo de compatibilidad de bases de datos está establecido en 90 o posterior. Al actualizar a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], las bases de datos de usuario conservan sus modos de compatibilidad. Antes de cambiar el modo de compatibilidad de bases de datos al 90 o posterior, cambie el nombre del objeto que contiene el carácter 0xFFFF.  
  
 Para obtener más información acerca de los identificadores, vea "Identificadores" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre los modos de compatibilidad de la base de datos, vea "sp_dbcmptlevel" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
