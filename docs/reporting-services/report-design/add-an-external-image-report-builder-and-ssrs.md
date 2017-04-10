---
title: "Agregar una imagen externa (Generador de informes y SSRS) | Microsoft Docs"
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
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Agregar una imagen externa (Generador de informes y SSRS)
  Las imágenes externas pueden estar en un servidor de informes en modo nativo o en modo integrado de SharePoint, o en cualquier otro sitio web. Cuando se incluyen imágenes externas en un informe, se debe comprobar que existen y que el lector del informe dispone de los permisos necesarios para tener acceso a ella. Para más información, vea [Imágenes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Agregar una imagen externa  
  
1.  En la vista de diseño del informe, en la pestaña **Insertar** , haga clic en **Imagen**.  
  
2.  En la superficie de diseño, haga clic en un cuadro y, a continuación, arrástrelo hasta obtener el tamaño de la imagen que desee.  
  
3.  En la pestaña **General** del cuadro de diálogo **Propiedades de la imagen** , escriba un nombre en el cuadro de texto **Nombre** o acepte el nombre predeterminado.  
  
4.  (Opcional) En el cuadro de texto **Información sobre herramientas**, escriba el texto que se mostrará cuando el usuario mantenga el mouse sobre la imagen en un informe representado para HTML.  
  
5.  En **Seleccionar el origen de la imagen**, seleccione **Externo**.  
  
     Para una imagen en un servidor de informes en modo nativo, escriba la ruta de acceso relativa de la imagen en el cuadro **Usar esta imagen** (por ejemplo, ../images/image1.jpg).  
  
     Para una imagen en un servidor de informes en modo integrado de SharePoint (o cualquier otro sitio web), escriba la dirección URL completa de la imagen en el cuadro **Usar esta imagen** (por ejemplo, http://\<nombreServidorSharePoint>/\<sitio>/Documents/images/image1.jpg).  
  
     Para más información, vea [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Opcional) Haga clic en **Tamaño**, **Visibilidad**, **Acción** o **Borde** si quiere establecer propiedades adicionales para el elemento de informe de imagen.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Incrustar una imagen en un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Agregar una imagen de fondo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [Cuadro de diálogo de Propiedades de la imagen, General &#40;Generador de informes y SSRS&#41;](../Topic/Image%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  