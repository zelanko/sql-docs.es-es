---
title: Agregar, mover o eliminar una tabla, una matriz o una lista (Generador de informes y SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 99726dcd58f88075a6f9ffabdb419b1c46e9aee5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>Agregar, mover o eliminar una tabla, una matriz o una lista (Generador de informes y SSRS)
  En un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , una región de datos muestra los datos de un conjunto de datos de un informe. Entre las regiones de datos se incluyen las siguientes: tabla, matriz, lista, gráfico y medidor. Para anidar una región de datos dentro de otra, agregue por separado cada región de datos y, a continuación, arrastre la región de datos secundaria a la región de datos primaria.  
  
 La manera más simple de agregar una región de datos de tabla o de matriz a su informe es ejecutar el Asistente para nueva tabla o el Asistente para nueva matriz. Estos asistentes le guiarán en el proceso de elegir una conexión a un origen de datos, de organizar los campos y de elegir el diseño y el estilo. Los asistentes solamente están disponibles en el Generador de informes.  
  
## <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>Para agregar una tabla o una matriz a un informe utilizando el Asistente para nueva tabla o el Asistente para nueva matriz  
  
1.  En la pestaña **Insertar** , haga clic en **Tabla** o en **Matriz**y, a continuación, haga clic en **Asistente para tablas** o en **Asistente para matrices**.  
  
2.  Siga los pasos del Asistente para **Nueva tabla** o **Nueva matriz** .  
  
3.  En la pestaña **Inicio** , haga clic en **Ejecutar** para ver el informe representado.  
  
4.  En la pestaña **Ejecutar** , haga clic en **Diseño** para seguir trabajando en el informe.  
  
## <a name="to-add-a-data-region"></a>Para agregar una región de datos  
  
1.  En la **Cinta de opciones**, en el grupo **Regiones de datos** , haga clic en la región de datos que desea agregar.  
  
2.  Haga clic en la superficie de diseño y, a continuación, arrastre para crear un cuadro que tenga el tamaño deseado para la región de datos.  
  
3.  Arrastre un campo del conjunto de datos de informe desde el panel Datos de informe hasta una celda de la región de datos. La región de datos queda enlazada con los datos del conjunto de datos de informe.  
  
## <a name="to-select-a-data-region"></a>Para seleccionar una región de datos  
  
-   En el caso de una región de datos Tablix, haga clic con el botón secundario en el controlador de tabla. En el caso de un gráfico o una región de datos de medidor, haga clic en la región de datos.  
  
     Aparecerá un controlador de selección y ocho controladores de tamaño.  
  
     En el caso de regiones de datos anidadas, haga clic con el botón derecho en la región de datos anidada, haga clic en **Seleccionar**y, después, seleccione el elemento de informe que quiera. Para comprobar qué elemento de informe está seleccionado, use el panel de propiedades. El nombre del elemento seleccionado en la superficie de diseño aparece en la barra de herramientas del panel de propiedades.  
  
## <a name="to-move-a-data-region"></a>Para mover una región de datos  
  
-   Para mover una región de datos, haga clic en el controlador de selección de ésta y arrástrelo. Use las líneas de ajuste para alinearla con los elementos de informe existentes.  
  
     Si la regla no está visible, hace clic la pestaña Ver y selecciona la opción **Regla** .  
  
     Como alternativa, use las teclas de dirección para mover la región de datos seleccionada por la superficie de diseño.  
  
## <a name="to-delete-a-data-region"></a>Para eliminar una región de datos  
  
-   Seleccione la región de datos, haga clic con el botón derecho en ella y, después, haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
