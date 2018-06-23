---
title: Arquitectura de elementos de informe personalizados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
caps.latest.revision: 15
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4bb30b88a25739f5a5d67cb67a7522a0aeab8658
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104656"
---
# <a name="custom-report-item-architecture"></a>Arquitectura de elementos de informe personalizados
  Un elemento de informe personalizado es una extensión del lenguaje RDL (Report Definition Language) que permite a los programadores agregar la funcionalidad que no se admite de forma nativa en RDL o que extiende la funcionalidad de los controles existentes. Hay dos componentes principales en un elemento de informe personalizado: el componente de tiempo de ejecución y el componente de tiempo de diseño. Estos componentes se implementan como ensamblados de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y se pueden escribir en cualquier lenguaje compatible con CLS.  
  
## <a name="the-run-time-component"></a>Componente en tiempo de ejecución  
 El procesador de informes llama en tiempo de ejecución al componente de tiempo de ejecución para un elemento de informe personalizado. El componente de tiempo de ejecución acepta los datos que pasa en tiempo de ejecución el procesador del informe, procesa estos datos y devuelve una imagen que contiene el elemento de informe personalizado representado.  
  
 ![Componente en tiempo de ejecución del elemento de informe personalizado](../../../2014/reporting-services/media/customreportitemrun-timecomponentarchitecture.gif "Componente en tiempo de ejecución del elemento de informe personalizado")  
  
## <a name="the-design-time-component"></a>Componente de tiempo de diseño  
 El componente de tiempo de diseño permite definir y manipular el elemento de informe personalizado en la interfaz del Diseñador de informes en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. El componente de tiempo de diseño está compuesto de varios subcontroles que controlan la apariencia y las propiedades del elemento de informe personalizado en el entorno de diseño.  
  
 ![Componente en tiempo de diseño del elemento de informe personalizado](../../../2014/reporting-services/media/customreportitemdesign-timecomponentarchitecture.gif "Componente en tiempo de diseño del elemento de informe personalizado")  
  
## <a name="see-also"></a>Vea también  
 [Creación de un componente de tiempo de ejecución de elemento de informe personalizado](../custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Creación de un componente de tiempo de diseño de elemento de informe personalizado](../custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Implementación de un elemento de informe personalizado](../custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  