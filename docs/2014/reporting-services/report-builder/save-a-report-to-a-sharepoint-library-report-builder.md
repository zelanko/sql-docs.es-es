---
title: Guardar un informe en una biblioteca de SharePoint (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab4f9b06758d29ff1f988f37b95ce92206f34d39
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107676"
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>Guardar un informe en una biblioteca de SharePoint (Generador de informes)
  Para guardar un informe en un servidor de informes configurado para la integración de SharePoint, debe examinar el servidor de SharePoint y establecer una conexión con el servidor de informes. En la definición de informe, todas las referencias a los elementos relacionados con el informe deben utilizar valores que sean específicos de un servidor de informes de SharePoint. Los elementos relacionados incluyen subinformes, informes detallados y recursos como imágenes basadas en web. Para más información, vea [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](../report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Debe disponer del permiso **Miembro** o **Propietario** en el sitio de SharePoint para establecer las propiedades en el proyecto.  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>Guardar un informe en un sitio de SharePoint  
  
1.  Desde el botón Generador de informes, haga clic en **Guardar**. Se abre el cuadro de diálogo **Guardar como**_\<elemento de informe>_.  
  
    > [!NOTE]  
    >  Si vuelve a guardar un informe, automáticamente se guarda en su ubicación anterior. Utilice la opción **Guardar como** para cambiar la ubicación.  
  
2.  Si lo desea, puede hacer clic en **Sitios y servidores recientes** para mostrar una lista de servidores de informes y sitios de SharePoint utilizados recientemente.  
  
3.  Vaya al sitio de SharePoint y, a continuación, haga clic en **Guardar**.  
  
    > [!NOTE]  
    >  Si deja un informe cambiado durante más de diez horas sin guardarlo, se desconecta del servidor sin guardarse. Si ocurre esto, en la barra de estado inferior derecha, haga clic en **Desconectar**y, después, en **Conectar**. El servidor más reciente estará en la lista de servidores disponibles. Selecciónelo y el informe volverá a conectarse.  
  
## <a name="see-also"></a>Vea también  
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
