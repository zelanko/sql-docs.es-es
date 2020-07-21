---
title: Página de movimiento de elementos (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f64a9e9efe180c2db776c38553403e5f7cdfac9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108221"
---
# <a name="move-items-page-report-manager"></a>Mover elementos (página del Administrador de informes)
  Use la página Mover elementos para mover un informe, una carpeta u otro elemento a una nueva ubicación del servidor de informes. Puede escribir la ruta de acceso a la nueva ubicación o utilizar la vista de árbol para desplazarse hasta la nueva ubicación en el espacio de nombres del servidor de informes. Solo puede mover los elementos para los que tenga permiso para mover y que estén almacenados en el servidor de informes actual.  
  
 Cuando se mueve un elemento al que hace referencia otro elemento (por ejemplo, un modelo u origen de datos compartido al que hacen referencia muchos informes), la información de la ruta de acceso del elemento se actualiza de forma automática. Mover un origen de datos compartidos no afecta una conexión de origen de datos a los informes y los modelos que lo usan. Si mueve un modelo u origen de datos compartido a una carpeta para la que los usuarios no tienen permiso, todavía podrán ejecutar cualquier informe que haga referencia al modelo u origen de datos. Sin embargo, el modelo no estará visible para ellos en la jerarquía de carpetas.  
  
 Para **Ubicación**, especifique la ruta de acceso completa a la carpeta, empezando por el nombre de la carpeta raíz. Puede escribir el nombre de la ruta de acceso o utilizar la vista de árbol para navegar hasta la carpeta que desee.  
  
> [!NOTE]  
>  No todos los elementos pueden moverse. Las carpetas reservadas, como Inicio, Mis informes o Carpetas de usuarios, no se pueden mover. Los historiales de informe y las instantáneas no se pueden mover a otras ubicaciones. El historial y las instantáneas siempre se encuentran en la misma ubicación que el informe en el que se basan, y se obtiene acceso a ellos a través de dicho informe.  
  
## <a name="navigation"></a>Navegación  
 Utilice los procedimientos siguientes para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>Para abrir la página Mover elementos desde la página Contenido de la vista Detalles  
  
1.  Abra el Administrador de informes y navegue a la carpeta que contenga un elemento que desee mover. También puede mover elementos desde la página principal del Administrador de informes.  
  
2.  En la barra de herramientas, haga clic en **Vista Detalles**.  
  
    > [!NOTE]  
    >   Si únicamente aparece la **Vista en mosaico**, significa que ya se encuentra en la **Vista Detalles**.  
  
3.  Active la casilla situada junto a un elemento y, a continuación, haga clic en **Mover** en la barra de herramientas. Puede seleccionar más de una casilla si desea mover varios elementos a la misma nueva ubicación.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>Para abrir la página Mover elementos desde la página Contenido en la Vista en mosaico  
  
1.  Abra el Administrador de informes y navegue a la carpeta que contenga un elemento que desee mover. También puede mover elementos desde la página principal del Administrador de informes.  
  
2.  En la barra de herramientas, haga clic en **Vista en mosaico**.  
  
    > [!NOTE]  
    >   Si únicamente aparece la **Vista Detalles**, significa que ya se encuentra en la **Vista en mosaico**.  
  
3.  Mantenga el mouse sobre un elemento y haga clic en la flecha de lista desplegable.  
  
4.  En el menú desplegable, haga clic en **Mover**.  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>Para abrir la página Mover elementos desde la página Propiedades generales de un elemento  
  
1.  Abra el Administrador de informes y navegue a la carpeta que contenga un elemento que desee mover. También puede mover elementos desde la página principal del Administrador de informes.  
  
2.  Mantenga el mouse sobre un elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página Propiedades generales de un elemento.  
  
4.  En la barra de herramientas del elemento, haga clic en **Mover**.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página de propiedades generales, carpetas &#40;Administrador de informes&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [Página de propiedades generales, informes &#40;Administrador de informes&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Página de propiedades generales, recursos &#40;Administrador de informes&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 [Página de propiedades generales, orígenes de datos compartidos &#40;Administrador de informes&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
