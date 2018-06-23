---
title: Cambios de comportamiento de syslockinfo y sp_lock | Documentos de Microsoft
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
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 982f31bbffb32726089fa331d105bfc262fc16a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107531"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>Cambios del comportamiento de syslockinfo y sp_lock
  **syslockinfo** y **sp_lock** devolver valores inesperados. También pueden devolver filas adicionales, mientras que las versiones anteriores de **syslockinfo** y **sp_lock** devolvían un máximo de dos filas por recurso de bloqueo.  
  
 Para obtener acceso a la información de **syslockinfo** o para ejecutar **sp_lock** es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **rsc_objid** y **rsc_indid** columnas en **syslockinfo** y **objid** y **indid**  columnas en **sp_lock** devolver el identificador de objeto de forma coherente e Id. de índice En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible que se devuelva un valor de 0.  
  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], **syslockinfo** y **sp_lock** devolver un máximo de dos filas para cualquier recurso de bloqueo determinado en una sola transacción. A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], cuando está habilitada la partición del bloqueo, pueden devolverse varias filas del mismo recurso que se ejecuta en una sola transacción. Allí pueden hasta N + 1 filas devolver, donde N es el número de CPU. Asimismo, ahora es posible que se muestren solicitudes GRANTED y WAITING para el mismo recurso, lo cual no era posible en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
