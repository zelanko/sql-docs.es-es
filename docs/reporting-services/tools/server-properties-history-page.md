---
title: "Propiedades del servidor (página Historial) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
caps.latest.revision: "30"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 80fac6d5c466240ceb40fc7b6c4725fc94b252fd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="server-properties-history-page"></a>Propiedades del servidor (página Historial)
  Use esta página de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para establecer un valor predeterminado para el número de copias del historial de informes que es necesario conservar. El valor predeterminado proporciona un valor inicial que establece los límites del historial de informes para todos los informes. Existe la posibilidad de modificar esta configuración para informes individuales.  
  
 El historial de informes es una colección de instantáneas de informe que incluye datos de informe y diseño actual para el informe en el momento en que se crea la instantánea. Puede usar el historial de informes para mantener una copia de un informe como se encontraba en una fecha u hora específicas. Puede crear y administrar el historial de informes para informes individuales que se ejecutan en un servidor de informes en modo nativo o un servidor de informes que se configura para modo integrado con SharePoint.  
  
 Las instantáneas del historial de informes están almacenadas en la base de datos del servidor de informes. Si mantiene un número ilimitado de instantáneas, asegúrese de comprobar periódicamente el tamaño de la base de datos para asegurarse de que no crece demasiado rápido ni consume demasiado espacio en disco.  
  
 Para abrir esta página:
 1) Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Conéctese a una instancia del servidor de informes.
 3) Haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**.
 4) Haga clic en **Historial** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **Conservar un número ilimitado de instantáneas en el historial de informe**  
 Conserve todas las instantáneas del historial de informes. Para reducir el tamaño del historial de informe, debe eliminar las instantáneas manualmente.  
  
 **Limitar las copias del historial de informe**  
 Conserve un número fijo de instantáneas del historial de informes. Cuando se alcanza el límite, las copias más antiguas se eliminan del historial de informe para dejar sitio para las nuevas.  
  
 Si posteriormente limita el historial del informe, cuando el historial del informe existente exceda el límite especificado, el servidor de informes lo reducirá según el nuevo límite. Las instantáneas de informe más antiguas son las que se eliminan primero. Si el historial del informe está vacío o por debajo del límite, se agregan nuevas instantáneas de informe. Cuando se alcanza el límite, se elimina la instantánea del informe más antigua cuando se agrega una nueva.  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Servidor de informes en Management Studio (Ayuda F1)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
