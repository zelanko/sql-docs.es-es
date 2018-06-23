---
title: Propiedades de SQL Server Browser (pestaña Avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba79137a-cb72-4bf3-a650-e11d02cfce10
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 98dfc61d352f8769864e9566a6ca50a8c979e4e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103222"
---
# <a name="sql-server-browser-properties-advanced-tab"></a>Propiedades de SQL Server Browser (pestaña Avanzadas)
  El programa Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta como un servicio en el servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser escucha las solicitudes entrantes de recursos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y proporciona información acerca de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.  
  
## <a name="options"></a>Opciones  
 **Agrupado**  
 Indica si este servicio está instalado como un recurso de un servidor en clúster.  
  
 **Informes de comentarios de clientes**  
 Indica si se ha habilitado la supervisión de la calidad del servicio en este servicio. Para obtener más información acerca de los informes de comentarios de clientes, busque el tema sobre la configuración de informes de errores y uso en los Libros en pantalla.  
  
 **Volcar directorio**  
 Ubicación de los volcados de memoria si se produce un error.  
  
 **Informes de errores**  
 Cuando se establece en **Yes**, el programa Dr. Watson envía información a [!INCLUDE[msCoName](../../includes/msconame-md.md)] o a su servidor de errores si se produce un error grave. Para obtener más información acerca de Informes de errores, busque el tema sobre la configuración de informes de errores y uso en los Libros en pantalla.  
  
 **Id. de instancia**  
 Indica la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha usado esta instancia del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La instancia predeterminada es **MSSQL10_50.MSSQLSERVER**.  
  
## <a name="see-also"></a>Vea también  
 [Servicio SQL Server Browser](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  