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
ms.openlocfilehash: a6dfe3901cb23cff65dd96fa084232310ef91ede
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104575"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>Cambios del comportamiento de syslockinfo y sp_lock
  **syslockinfo** y **sp_lock** devolver valores inesperados. También pueden devolver filas adicionales, mientras que las versiones anteriores de **syslockinfo** y **sp_lock** devolvían un máximo de dos filas por recurso de bloqueo.  
  
 Para obtener acceso a la información de **syslockinfo** o para ejecutar **sp_lock** es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **rsc_objid** y **rsc_indid** columnas en **syslockinfo** y **objid** y **indid**  columnas en **sp_lock** devuelven el identificador de objeto sistemáticamente y el Id. de índice En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible que se devuelva un valor de 0.  
  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** y **sp_lock** devolver un máximo de dos filas para cualquier recurso de bloqueo dado en una sola transacción. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], cuando está habilitada la partición del bloqueo, pueden devolverse varias filas del mismo recurso que se ejecuta en una sola transacción. Allí pueden hasta N + 1 filas devolverse, donde N es el número de CPU. Asimismo, ahora es posible que se muestren solicitudes GRANTED y WAITING para el mismo recurso, lo cual no era posible en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
