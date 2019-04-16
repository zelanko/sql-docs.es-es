---
title: Los cambios en el comportamiento de syslockinfo y sp_lock | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4e2fa557efb6f09eae78180390c733f35bdc4a17
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582281"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>Cambios del comportamiento de syslockinfo y sp_lock
  **syslockinfo** y **sp_lock** devolver valores inesperados. También pueden devolver filas adicionales, mientras que las versiones anteriores de **syslockinfo** y **sp_lock** devolvían un máximo de dos filas por recurso de bloqueo.  
  
 Para obtener acceso a la información de **syslockinfo** o para ejecutar **sp_lock** es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], las columnas **rsc_objid** y **rsc_indid** en **syslockinfo** y las columnas **objid** e **indid** en **sp_lock** devuelven sistemáticamente el Id. de objeto y el Id. de índice. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible que se devuelva un valor de 0.  
  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** y **sp_lock** devuelven un máximo de dos filas para un recurso de bloqueo dado en una transacción única. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], cuando está habilitada la partición del bloqueo, pueden devolverse varias filas del mismo recurso que se ejecuta en una sola transacción. Allí pueden hasta N + 1 filas devolverse, donde N es el número de CPU. Asimismo, ahora es posible que se muestren solicitudes GRANTED y WAITING para el mismo recurso, lo cual no era posible en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
