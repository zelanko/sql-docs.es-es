---
title: "Propiedades del servidor (p&#225;gina Ejecuci&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.reportserver.serverproperties.execution.f1"
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# Propiedades del servidor (p&#225;gina Ejecuci&#243;n)
  Utilice esta página para establecer un valor de tiempo de espera para la ejecución de informes. Este valor se aplica a todos los informes que se procesan mediante la instancia del servidor de informes actual. Puede sobrescribir este valor para informes individuales. El valor que especifica debe alojar todo el procesamiento de informes que se produce en el servidor de informes, más el procesamiento de consultas realizado en el servidor de bases de datos cuando el servidor de informes recupera datos que se usan en el informe.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Ejecución** para abrir esta página.  
  
## Opciones  
 **No establecer tiempo de espera para la ejecución de informes**  
 Permite a un servidor de informes tiempo ilimitado para completar el procesamiento de informes.  
  
 **Limitar la ejecución de informes al siguiente número de segundos**  
 Establezca una restricción horaria en la ejecución de informes. El período de tiempo empieza cuando se solicita el informe. Si el período finaliza antes de que el informe se haya procesado completamente, el servidor de informes cancela el proceso y todas las consultas en proceso para orígenes de datos externos.  
  
## Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  