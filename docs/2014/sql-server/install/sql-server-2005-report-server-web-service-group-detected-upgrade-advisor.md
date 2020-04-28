---
title: SQL Server el grupo de servicios web del servidor de informes 2005 detectado (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bfeff5eae569b481edfcc1cacc89c26e44edaece
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952373"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Se ha detectado el grupo de servicio web del servidor de informes de SQL Server 2005 (Asesor de actualizaciones)
  El asesor de actualizaciones ha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectado que la instancia está [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] asociada a un grupo de servicios web del servidor de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no utiliza el grupo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] de servicios web del servidor de informes. Al actualizar de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], este grupo de servicio se elimina y las listas de control de acceso (ACL) personalizadas para este grupo o los usuarios que pertenecen al grupo no se conservan durante la actualización.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de ejecutar la actualización, realice una copia de seguridad de las ACL o usuarios personalizados que pertenecen al grupo de servicio web del servidor de informes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para ello, puede usar la herramienta de línea de comandos **icacls. exe** en [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 y versiones posteriores, o la herramienta de línea de comandos cacls. exe en sistemas operativos Windows [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] anteriores a SP2. Para obtener más información sobre la sintaxis de estas herramientas, vea la documentación del producto de Windows. Una vez completado correctamente el programa de instalación, aplique las ACL o los usuarios personalizados al grupo de Windows Servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para la instancia del servidor de informes. El [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] grupo de Windows del servidor de informes adopta la forma\<de SQLServerReportServerUser $*computer_name*>$\<*instance_name*>.  
  
## <a name="see-also"></a>Consulte también  
 [Reporting Services problemas de actualización &#40;el asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
