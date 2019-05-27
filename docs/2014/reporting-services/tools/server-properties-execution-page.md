---
title: Propiedades del servidor (página Ejecución) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f0ec8725a0cec9e15cb6d8402f8d654320c38471
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099600"
---
# <a name="server-properties-execution-page"></a>Propiedades del servidor (página Ejecución)
  Utilice esta página para establecer un valor de tiempo de espera para la ejecución de informes. Este valor se aplica a todos los informes que se procesan mediante la instancia del servidor de informes actual. Puede sobrescribir este valor para informes individuales. El valor que especifica debe alojar todo el procesamiento de informes que se produce en el servidor de informes, más el procesamiento de consultas realizado en el servidor de bases de datos cuando el servidor de informes recupera datos que se usan en el informe.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia del servidor de informes, haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**. Haga clic en **Ejecución** para abrir esta página.  
  
## <a name="options"></a>Opciones  
 **No establecer tiempo de espera para la ejecución de informes**  
 Permite a un servidor de informes tiempo ilimitado para completar el procesamiento de informes.  
  
 **Limitar la ejecución de informes al siguiente número de segundos**  
 Establezca una restricción horaria en la ejecución de informes. El período de tiempo empieza cuando se solicita el informe. Si el período finaliza antes de que el informe se haya procesado completamente, el servidor de informes cancela el proceso y todas las consultas en proceso para orígenes de datos externos.  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Establecer las propiedades del procesamiento de informes](../report-server/set-report-processing-properties.md)   
 [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)  
  
  
