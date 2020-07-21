---
title: Cambios en el comportamiento de syslockinfo y sp_lock | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 65ace190004cab911dd8996642720620eba94935
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045155"
---
# <a name="changes-to-behavior-in-syslockinfo-and-sp_lock"></a>Cambios del comportamiento de syslockinfo y sp_lock
  **syslockinfo** y **sp_lock** devolver valores inesperados. También pueden devolver filas adicionales, mientras que las versiones anteriores de **syslockinfo** y **sp_lock** devolvían un máximo de dos filas por recurso de bloqueo.  
  
 Para obtener acceso a la información de **syslockinfo** o para ejecutar **sp_lock** es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], las columnas **rsc_objid** y **rsc_indid** en **syslockinfo** y las columnas **objid** e **indid** en **sp_lock** devuelven sistemáticamente el Id. de objeto y el Id. de índice. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible que se devuelva un valor de 0.  
  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** y **sp_lock** devuelven un máximo de dos filas para un recurso de bloqueo dado en una transacción única. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], cuando está habilitada la partición del bloqueo, pueden devolverse varias filas del mismo recurso que se ejecuta en una sola transacción. Puede haber hasta N + 1 filas devueltas, donde N es el número de CPU. Asimismo, ahora es posible que se muestren solicitudes GRANTED y WAITING para el mismo recurso, lo cual no era posible en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
