---
title: Buscar elementos de informe y establecer una carpeta predeterminada (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2eef96c7bde16746a91fe53f94adb19bbadadf2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581829"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>Buscar elementos de informe y establecer una carpeta predeterminada (Generador de informes y SSRS)
La manera más fácil de crear un informe paginado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es agregar elementos de informe existentes, como tablas y gráficos, desde la galería de elementos de informe. Al agregar un elemento de informe al informe, también agrega todo lo que debe tener para que funcione. Por ejemplo, cualquier elemento de informe que muestre los datos depende de un conjunto de datos, es decir, una consulta y una conexión a un origen de datos. Después de agregar el elemento de informe a un informe, puede modificarlo como convenga.  
  
 Puede establecer una carpeta predeterminada para publicar elementos de informe en el servidor de informes o el sitio de SharePoint integrado con un servidor de informes.  
  
 Para más información, vea [Elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
## <a name="to-browse-for-report-parts"></a>Para buscar elementos de informe  
  
1.  En el menú **Insertar** , haga clic en **Elementos de informe**.  
  
     Si no está conectado, haga clic en **Conectar con un servidor de informes**y escriba el nombre.  
  
    > [!NOTE]  
    >  Debe estar conectado a un servidor de informes para buscar elementos de informe.  
  
2.  Puede restringir la búsqueda especificando detalles sobre el elemento de informe. Escriba todo o parte del nombre y la descripción en el cuadro **Buscar** , o haga clic **Agregar criterios** y agregue los valores para alguno de los campos o para todos:  
  
    -   Creado por  
  
    -   Fecha de creación  
  
    -   Fecha de última modificación  
  
    -   Última modificación por  
  
    -   Carpeta del servidor  
  
    -   Tipo  
  
     Por ejemplo, para encontrar una imagen, haga clic en **Agregar criterios**y, a continuación, haga clic en **Tipo**. En la lista desplegable, active la casilla **Imagen** , presione ENTRAR y, a continuación, haga clic en la lupa de Buscar.  
  
    > [!NOTE]  
    >  Para los valores de **Creado por** y **Última modificación por** , busque el nombre de usuario de la persona como se representa en el servidor de informes.  
  
## <a name="to-set-a-default-folder-for-report-parts"></a>Para establecer una carpeta predeterminada para elementos de informe  
  
1.  Haga clic en **Generador de informes**y, a continuación, en **Opciones**.  
  
2.  En el cuadro de diálogo **Opciones** , en la pestaña **Configuración** , escriba un nombre de carpeta en el cuadro de texto **Publicar elementos de informe en esta carpeta de forma predeterminada** .  
  
 El Generador de informes creará esta carpeta si se dispone de permisos para crear carpetas en el servidor de informes y la carpeta no existe todavía.  
  
 No necesita reiniciar el Generador de informes para que esta configuración surta efecto.  
  
## <a name="see-also"></a>Consulte también  
 [Seleccionar o anular la selección de actualizaciones (Generador de informes y SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Elementos de informe y conjuntos de datos en el Generador de informes](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Solucionar problemas de elementos de informe (Generador de informes y SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Publicar y volver a publicar elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
