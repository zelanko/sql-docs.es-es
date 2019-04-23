---
title: Vincular un informe a un modelo como informe Click-through | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- customizing clickthrough reports
- clickthrough reports, customizing
- clickthrough reports, templates
ms.assetid: 3af42de3-67ef-41c2-bc8a-7045baec6f63
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 90b21c6fa21322afe1d9351e73460fce1a4592f8
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944161"
---
# <a name="link-a-report-to-a-model-as-a-clickthrough-report"></a>Vincular un informe a un modelo como informe click-through
  En lugar de utilizar las plantillas del informe click-through predeterminadas, puede crear un informe del Generador de informes y, a continuación, hacer clic en una entidad específica en el modelo de informe. Cuando la persona que ve el informe hace clic en los datos interactivos del informe principal, éste se muestra como un informe click-through. Para vincular un informe a una entidad, utilice el Administrador de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  La entidad principal o base que se utiliza en el informe debe ser la misma a la que está vinculado el informe.  
  
### <a name="to-start-report-manager-from-a-browser"></a>Para iniciar el Administrador de informes desde un explorador  
  
1.  Abra [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 6.0 o posterior.  
  
2.  En la barra de direcciones del explorador web, escriba la dirección URL del Administrador de informes. De forma predeterminada, la dirección URL es http://\<*ComputerName*> / reports.  
  
### <a name="to-create-a-customized-clickthrough-report"></a>Para crear un informe click-through personalizado  
  
1.  Navegue al modelo de informe al que desea agregar el informe click-through personalizado.  
  
2.  Haga doble clic en el modelo de informe.  
  
3.  Haga clic en **Click-through**.  
  
4.  Seleccione la entidad a la que desea adjuntar el informe click-through personalizado.  
  
    > [!NOTE]  
    >  Esta entidad debe ser igual que la entidad base del informe click-through personalizado.  
  
5.  Para mostrar el informe personalizado cuando se hace clic en una sola instancia de la entidad seleccionada, haga clic en el botón **Examinar** del informe de una sola instancia.  
  
     -o bien-  
  
     Para mostrar el informe personalizado cuando se hace clic en varias instancias de la entidad seleccionada, haga clic en el botón **Examinar** del informe de varias instancias.  
  
6.  Seleccione el informe y, a continuación, haga clic en **Aceptar**.  
  
7.  Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Vea también  
 [Informes Click-through &#40;SSRS&#41;](reports/clickthrough-reports-ssrs.md)  
  
  
