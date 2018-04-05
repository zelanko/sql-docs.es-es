---
title: Agregar un informe nuevo o existente a un proyecto de informe (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e29acdb16ec95fa3e2504cef099e26f55b82b792
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>Agregar un informe nuevo o existente a un proyecto de informe (SSRS)
  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede agregar un nuevo informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] usando el Asistente para informes o agregando un nuevo informe en blanco al proyecto. También puede agregar un informe existente. Después de agregar un informe, puede ver el nombre de informe en la lista que se muestra bajo la carpeta **Informes** del proyecto.  
  
> [!NOTE]  
>  Para obtener la vista previa de un informe con orígenes de datos existentes, debe tener permisos en el origen de datos del cliente de creación de informes. Para obtener más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Después de agregar un informe, puede definir orígenes de datos, conjuntos de datos y establecer un diseño de informe. Para comenzar, vea [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) y [Tablas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>Para agregar un nuevo informe utilizando el Asistente para informes  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta Informes y, después, haga clic en **Agregar nuevo informe**. Se abrirá el cuadro de diálogo **Asistente para informes** .  
  
     Los pasos del asistente le guiarán a lo largo del proceso de creación de un origen de datos, creación de un conjunto de datos con una consulta, definición de grupos, especificación de un diseño y creación del informe. Entre estos pasos se incluyen los siguientes:  
  
    -   **Seleccionar un origen de datos.** El primer paso para crear un informe es definir un origen de datos. El Asistente para informes muestra una lista de todos los orígenes de datos compartidos del proyecto de informe y, además, una opción para crear un nuevo origen de datos.  
  
    -   **Diseñar una consulta.** El siguiente paso es diseñar una consulta. Puede escribir la cadena de consulta, compilarla mediante el Diseñador de consultas o importar una consulta de otro informe. Para obtener información acerca de Diseñador de consultas, vea [Reporting Services Query Designers](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835).  
  
    -   **Elegir un tipo de informe.** El siguiente paso es seleccionar el tipo de informe que desea. Puede elegir un informe tabular o de matriz. Un informe tabular tiene un número fijo de columnas. Un informe de matriz, o tabla de referencias cruzadas, tiene un número variable de columnas en función de los resultados de la consulta. Un informe de mapa muestra datos analíticos con un fondo geográfico.  
  
    -   **Asignar nombre al informe.**  El paso final es asignar un nombre al informe y comprobar los campos que se incluirán en el mismo. Una vez completados todos los pasos, el Diseñador de informes crea el informe y lo agrega al proyecto del servidor de informes.  
  
## <a name="to-add-a-new-blank-report"></a>Para agregar un nuevo informe en blanco  
  
1.  En el menú **Proyecto** , haga clic en **Agregar nuevo elemento**.  
  
2.  En **Plantillas**, haga clic en **Informe**.  
  
3.  Haga clic en **Agregar**.  
  
     Se agregará un nuevo informe en blanco al proyecto y se mostrará en la superficie de diseño.  
  
## <a name="to-add-an-existing-report"></a>Para agregar un informe existente  
  
1.  En el menú **Proyecto** , haga clic en **Agregar**y, a continuación, haga clic en  **Existing Item**(Elemento existente).  
  
2.  Navegue a la ubicación del archivo .rdl, selecciónelo y, a continuación, haga clic en **Agregar**.  
  
     El informe se agregará al proyecto bajo la carpeta **Informes** . Cuando cierre y vuelva a abrir el proyecto, los informes se mostrarán ordenados alfabéticamente.  
  
## <a name="see-also"></a>Ver también  
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 ¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
  
  
