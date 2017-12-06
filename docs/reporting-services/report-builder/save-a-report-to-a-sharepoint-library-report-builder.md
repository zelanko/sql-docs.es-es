---
title: Guardar un informe en una biblioteca de SharePoint (Generador de informes) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 40d1a1ca553cbc14517a4850d116ad1ee15f805d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>Guardar un informe en una biblioteca de SharePoint (Generador de informes)
  Para guardar un informe en un servidor de informes configurado para la integración de SharePoint, debe examinar el servidor de SharePoint y establecer una conexión con el servidor de informes. En la definición de informe, todas las referencias a los elementos relacionados con el informe deben utilizar valores que sean específicos de un servidor de informes de SharePoint. Los elementos relacionados incluyen subinformes, informes detallados y recursos como imágenes basadas en web. Para más información, vea [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint para establecer las propiedades en el proyecto.  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>Guardar un informe en un sitio de SharePoint  
  
1.  Desde el botón Generador de informes, haga clic en **Guardar**. Se abre el cuadro de diálogo **Guardar como***\<elemento de informe>*.  
  
    > [!NOTE]  
    >  Si vuelve a guardar un informe, automáticamente se guarda en su ubicación anterior. Utilice la opción **Guardar como** para cambiar la ubicación.  
  
2.  Si lo desea, puede hacer clic en **Sitios y servidores recientes** para mostrar una lista de servidores de informes y sitios de SharePoint utilizados recientemente.  
  
3.  Vaya al sitio de SharePoint y, a continuación, haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Si deja un informe cambiado durante más de diez horas sin guardarlo, se desconecta del servidor sin guardarse. Si ocurre esto, en la barra de estado inferior derecha, haga clic en **Desconectar**y, después, en **Conectar**. El servidor más reciente estará en la lista de servidores disponibles. Selecciónelo y el informe volverá a conectarse.  
  
## <a name="see-also"></a>Vea también  
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
