---
title: Arquitectura de elementos de informe personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: ''
ms.component: custom-report-items
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
caps.latest.revision: 16
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 23489c20aa2e2d4da801134bc11383d6035286ea
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="custom-report-item-architecture"></a>Arquitectura de elementos de informe personalizados
  Un elemento de informe personalizado es una extensión del lenguaje RDL (Report Definition Language) que permite a los programadores agregar la funcionalidad que no se admite de forma nativa en RDL o que extiende la funcionalidad de los controles existentes. Hay dos componentes principales en un elemento de informe personalizado: el componente de tiempo de ejecución y el componente de tiempo de diseño. Estos componentes se implementan como ensamblados de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y se pueden escribir en cualquier lenguaje compatible con CLS.  
  
## <a name="the-run-time-component"></a>Componente en tiempo de ejecución  
 El procesador de informes llama en tiempo de ejecución al componente de tiempo de ejecución para un elemento de informe personalizado. El componente de tiempo de ejecución acepta los datos que pasa en tiempo de ejecución el procesador del informe, procesa estos datos y devuelve una imagen que contiene el elemento de informe personalizado representado.  
  
 ![Componente en tiempo de ejecución del elemento de informe personalizado](../../reporting-services/custom-report-items/media/customreportitemrun-timecomponentarchitecture.gif "Componente en tiempo de ejecución del elemento de informe personalizado")  
  
## <a name="the-design-time-component"></a>Componente de tiempo de diseño  
 El componente de tiempo de diseño permite definir y manipular el elemento de informe personalizado en la interfaz del Diseñador de informes en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. El componente de tiempo de diseño está compuesto de varios subcontroles que controlan la apariencia y las propiedades del elemento de informe personalizado en el entorno de diseño.  
  
 ![Componente en tiempo de diseño del elemento de informe personalizado](../../reporting-services/custom-report-items/media/customreportitemdesign-timecomponentarchitecture.gif "Componente en tiempo de diseño del elemento de informe personalizado")  
  
## <a name="see-also"></a>Ver también  
 [Creación de un componente de tiempo de ejecución de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Creación de un componente de tiempo de diseño de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Implementación de un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
