---
title: Vista de diseño | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.layoutview.f1
helpviewer_keywords:
- Layout View dialog box
ms.assetid: 6fa378aa-442f-4d2f-beab-02a0fb5cd3ce
caps.latest.revision: 37
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: a7f9b00eec64ae93fdb60fa0f7f6e591087d039a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106506"
---
# <a name="design-view"></a>Vista de diseño
  Utilice la vista Diseño para organizar los elementos de informe en el informe. En ocasiones, la vista Diseño se conoce como vista de presentación o vista de superficie de diseño.  
  
## <a name="report-design-surface"></a>Superficie de diseño del informe  
 La superficie de diseño está formada por tres secciones: cuerpo del informe, encabezado de página y pie de página. Use el Cuadro de herramientas para seleccionar los elementos que desee colocar en cualquiera de estas tres secciones. Utilice el panel Datos de informe para ver las imágenes, los parámetros, los orígenes de datos y los conjuntos de datos, incluidas las consultas de conjunto de datos y las listas de campos. Después de agregar elementos de informe a la superficie de diseño, arrastre campos de conjunto de datos desde el panel **Datos de informe** hasta las regiones de datos como tabla, matriz o lista. Cada elemento de la superficie de diseño del informe contiene propiedades que se pueden administrar usando un cuadro de diálogo de propiedades o el panel Propiedades.  
  
## <a name="toolbox"></a>Cuadro de herramientas  
 El Cuadro de herramientas muestra las regiones de datos y otros elementos de informe que están disponibles para el informe. Para agregar elementos de informe del Cuadro de herramientas, haga doble clic en el elemento o arrástrelo hacia la superficie de diseño. A continuación puede cambiar la forma y tamaño utilizando los controladores de objeto.  
  
## <a name="report-data-pane"></a>panel Datos de informe  
 Para ver el panel Datos de informe, en el menú **Ver** , haga clic en **Datos de informe**. Utilice este panel para definir parámetros, imágenes, orígenes de datos y conjuntos de datos, y para hacer referencia a los campos integrados como ReportName. Para agregar un elemento nuevo, haga clic en el menú **Nuevo** y seleccione un elemento. Para agregar campos calculados a un conjunto de datos existente, haga clic en **Conjunto de datos**y, en el cuadro de diálogo **Propiedades del conjunto de datos** , seleccione **Campos**. Seleccione un elemento y haga clic en **Edición** para abrir el cuadro de diálogo **Propiedades** . También puede hacer clic con el botón secundario en los elementos del panel Datos de informe para agregarlos o actualizar sus propiedades.  
  
 Arrastre los elementos del panel Datos de informe a las regiones de datos y cuadros de texto de la superficie de diseño para agregar datos e imágenes a un informe.  
  
 Para más información, consulte [Report Data Pane](../report-data/report-data-pane.md).  
  
## <a name="grouping-pane"></a>Panel de agrupación  
 Los grupos se utilizan para organizar los datos del informe en una jerarquía visual y calcular los totales. Utilice el panel de agrupación para ver los grupos definidos para una tabla, matriz o región de datos de la lista. De forma predeterminada, el panel de agrupación muestra todos los grupos para la región de datos seleccionada como una lista sin información de estructura jerárquica. El panel de agrupación está deshabilitado para las regiones de datos Gráfico y Medidor.  
  
 Para comprobar si los grupos están relacionados entre sí, cambie el panel de agrupación al modo avanzado. Este modo muestra la jerarquía de miembros del grupo, una presentación visual de las celdas de la región de datos que corresponden a cada grupo.  
  
 Para obtener más información, vea [Grouping Pane](grouping-pane.md).  
  
## <a name="page-header-and-page-footer"></a>Encabezado y pie de página  
 Un encabezado y un pie de página aparecen en la parte superior e inferior de cada página, respectivamente. Los encabezados y pies de página pueden contener texto estático, imágenes, líneas, rectángulos, bordes, color de fondo e imágenes de fondo. Para agregar elementos de informe al encabezado o al pie de página, haga clic con el botón secundario en la superficie de diseño y seleccione Encabezado o Pie de página. Las secciones de encabezado y de pie de página aparecen en la superficie de diseño.  
  
## <a name="properties-pane"></a>Panel Propiedades  
 Utilice el panel Propiedades para ver las propiedades del elemento de informe seleccionado en la superficie de diseño o el grupo seleccionado en el panel de agrupación. También puede hacer clic con el botón derecho en un elemento de informe o grupo seleccionado y hacer clic después en **Propiedades** para abrir el cuadro de diálogo **Propiedades** correspondiente del elemento de informe o grupo.  
  
## <a name="see-also"></a>Vea también  
 [Encabezados y pies de página &#40;el generador de informes SSRS&#41;](../report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Sugerencias para el diseño de informes &#40;Generador de informes y SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md)  
  
  