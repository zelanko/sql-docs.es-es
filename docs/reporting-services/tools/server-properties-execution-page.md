---
title: Propiedades del servidor (página Ejecución) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.suite: pro-bi
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dcd23b60ff63083a75719a3786fb4b19a783211e
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272654"
---
# <a name="server-properties-execution-page"></a>Propiedades del servidor (página Ejecución)
  Utilice esta página para establecer un valor de tiempo de espera para la ejecución de informes. Este valor se aplica a todos los informes que se procesan mediante la instancia del servidor de informes actual. Puede sobrescribir este valor para informes individuales. El valor que especifica debe alojar todo el procesamiento de informes que se produce en el servidor de informes, más el procesamiento de consultas realizado en el servidor de bases de datos cuando el servidor de informes recupera datos que se usan en el informe.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Ejecución** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **No establecer tiempo de espera para la ejecución de informes**  
 Permite a un servidor de informes tiempo ilimitado para completar el procesamiento de informes.  
  
 **Limitar la ejecución de informes al siguiente número de segundos**  
 Establezca una restricción horaria en la ejecución de informes. El período de tiempo empieza cuando se solicita el informe. Si el período finaliza antes de que el informe se haya procesado completamente, el servidor de informes cancela el proceso y todas las consultas en proceso para orígenes de datos externos.  
  
## <a name="see-also"></a>Ver también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Servidor de informes en Management Studio (Ayuda F1)](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
