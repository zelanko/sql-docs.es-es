---
title: Permitir que un cuadro de texto crezca o se reduzca (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dbc01e78-5993-47e5-af04-34f9e3bbcee1
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: abb928e42a7420b421c91f6b5f78256213cb5df9
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs"></a>Permitir que un cuadro de texto aumente o se reduzca (Generador de informes y SSRS)
  En un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , los cuadros de texto no son simplemente los cuadros independientes de la superficie de diseño del informe. Cada celda de una tabla o una matriz (una región de datos de Tablix) contienen un cuadro de texto, al que se puede dar formato de la misma manera que a los cuadros de texto independientes. De manera predeterminada, los cuadros de texto son de tamaño fijo. Puede establecer las opciones que permiten que el cuadro de texto se expanda o se reduzca según su contenido. Estas opciones corresponden a las propiedades **CanGrow** o **CanShrink** del panel de propiedades.  
  
## <a name="to-allow-a-text-box-to-grow-or-shrink"></a>Permitir que un cuadro de texto crezca o se reduzca  
  
1.  Haga clic con el botón derecho en el cuadro y, después, haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en la pestaña **General** .  
  
    -   Para permitir que el cuadro de texto se expanda verticalmente en función de su contenido, seleccione **Permitir aumentar el alto**.  
  
    -   Para permitir que el cuadro de texto se reduzca en función del contenido, seleccione **Permitir reducir el alto**.  
  
## <a name="see-also"></a>Vea también  
 [Cuadros de texto &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)  
  
  
