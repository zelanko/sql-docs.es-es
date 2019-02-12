---
title: Usar Mis suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ddbb228cf4f5d71df60dd1de73ab0d1484925f70
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040796"
---
# <a name="use-my-subscriptions"></a>Usar Mis suscripciones
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] El Administrador de informes incluye un **Mis suscripciones** página que organiza todas las suscripciones en un solo lugar. Puede utilizar Mis suscripciones para ver, modificar y eliminar suscripciones existentes. Sin embargo, no puede utilizar esta página para crear suscripciones.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] |  
  
 En Mis suscripciones, puede ordenar las suscripciones por carpeta, informe, descripción, desencadenador, última ejecución o estado. Todos los valores se ordenan alfabéticamente, a excepción de Última ejecución, que utiliza el orden cronológico.  
  
 Mis suscripciones solo muestra las suscripciones que haya creado. No enumera las suscripciones que sean propiedad de otros usuarios, aunque el usuario esté agregado como suscriptor a ellas, ni muestra suscripciones controladas por datos.  
  
 No puede buscar suscripciones por nombre, ni tampoco basándose en información del desencadenador, información de estado, etc. Para obtener más información, consulte [crear, modificar y eliminar suscripciones estándar &#40;Reporting Services en modo nativo&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
## <a name="how-to-use-my-subscriptions"></a>Cómo usar Mis suscripciones  
 Mis suscripciones se encuentra disponible mediante el Administrador de informes. Para obtener acceso a Mis suscripciones, haga clic en **Mis suscripciones** en la barra de herramientas global del Administrador de informes.  
  
## <a name="use-windows-powershell-to-list-mysubscriptions"></a>Usar Windows PowerShell para enumerar MySubscriptions  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")  
  
 El siguiente script de PowerShell devolverá la lista de suscripciones y propiedades de suscripción del usuario actual. Para obtener más información, vea [ReportingService2010.ListMySubscriptions (Método)](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Suscripciones controladas por datos](data-driven-subscriptions.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Creación y administración de suscripciones para servidores de informes en modo nativo](../create-manage-subscriptions-native-mode-report-servers.md)  
  
  
