---
title: Se ha detectado el grupo de servicio Web de servidor de informes de SQL Server 2005 (Asesor de actualizaciones) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 7d3affeac1976b82ba269c4d86eac94cdc04335f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204075"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Se ha detectado el grupo de servicio web del servidor de informes de SQL Server 2005 (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia está asociada con un [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] grupo de servicio Web del servidor de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no usa el [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] grupo de servicio Web del servidor de informes. Al actualizar de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], este grupo de servicio se elimina y las listas de control de acceso (ACL) personalizadas para este grupo o los usuarios que pertenecen al grupo no se conservan durante la actualización.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de ejecutar la actualización, realice una copia de seguridad de las ACL o usuarios personalizados que pertenecen al grupo de servicio web del servidor de informes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para ello, puede usar el **Icacls.exe** herramienta de línea de comandos de [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 y versiones posteriores o la herramienta de línea de comandos Cacls.exe en sistemas operativos de Windows anteriores a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2. Para obtener más información sobre la sintaxis de estas herramientas, vea la documentación del producto de Windows. Una vez completado correctamente el programa de instalación, aplique las ACL o los usuarios personalizados al grupo de Windows Servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para la instancia del servidor de informes. El [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] grupo de Windows del servidor de informes toma la forma de SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  