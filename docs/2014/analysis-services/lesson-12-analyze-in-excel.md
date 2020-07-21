---
title: 'Lección 13: analizar en Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
author: minewiskan
ms.author: owend
ms.openlocfilehash: 509f44565a1535e1502cb3862250cf04f654711e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543547"
---
# <a name="lesson-13-analyze-in-excel"></a>Lección 13: Analizar en Excel
  En esta lección, usará la característica Analizar en Excel de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para abrir Microsoft Excel, crear automáticamente una conexión de origen de datos al área de trabajo del modelo y agregará automáticamente una tabla dinámica a la hoja de cálculo. La característica Analizar en Excel está pensada para proporcionar una manera rápida y sencilla de probar la eficacia del diseño del modelo antes de implementarlo. No realizará ningún análisis de datos en esta lección. El propósito de esta lección es conseguir que se familiarice, como autor del modelo, con las herramientas que puede usar para probar el diseño del modelo. Los usuarios finales no utilizarán la característica Analizar de Excel, que está destinada a los autores de modelos, sino que usarán aplicaciones de informes de cliente como Excel o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] para conectarse a los datos del modelo implementados y explorarlos.  
  
 Para completar esta lección, Excel se debe instalar en el mismo equipo que [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Para obtener más información, consulte [Analizar en Excel &#40;SSAS tabular&#41;](tabular-models/analyze-in-excel-ssas-tabular.md).  
  
 Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 11: Crear particiones](lesson-10-create-partitions.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Examinar mediante las perspectivas predeterminada y Venta por Internet  
 En estas primeras tareas, examinará su modelo con la perspectiva predeterminada, que incluye todos los objetos del modelo, y también con la perspectiva Venta por Internet que creó en la lección 8: Crear perspectivas. La perspectiva Venta por Internet excluye el objeto de tabla Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para examinar mediante la perspectiva predeterminada  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y después en **Analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel**, haga clic en **Aceptar**.  
  
     Se abrirá Excel con un nuevo libro. Se crea una conexión de origen de datos con la cuenta de usuario actual y se utiliza la perspectiva predeterminada para definir los campos visibles. Se agrega automáticamente una tabla dinámica a la hoja de cálculo.  
  
3.  En Excel, en la **lista de campos de la tabla dinámica**, observe que aparecen las medidas **fecha** y **venta por Internet** , así como las tablas **Customer**, **Date**, **Geography**, **Product**, Product **Category**, **Product subcategory**y **Internet sales** con todas sus columnas respectivas.  
  
4.  Cierre Excel sin guardar el libro.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para examinar mediante la perspectiva Venta por Internet  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y después en **Analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , mantenga seleccionado **Usuario de Windows actual** y, después, en el cuadro de lista desplegable **Perspectiva** , seleccione **Venta por Internet**y haga clic en **Aceptar**. Se abre Excel.  
  
3.  En Excel, en la **Lista de campos de tabla dinámica**, observe que la tabla Cliente se ha excluido de la lista de campos.  
  
## <a name="browse-using-roles"></a>Examinar con roles  
 Los roles son una parte integral de cualquier modelo tabular. Sin al menos un rol, al que se agregan usuarios en calidad de miembros, los usuarios no podrán tener acceso a los datos ni analizarlos con el modelo. La característica Analizar de Excel proporciona una manera de probar los roles que ha definido.  
  
#### <a name="to-browse-by-using-the-internet-sales-manager-user-role"></a>Para examinar con el rol de usuario Administrador de ventas por Internet  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo** y después en **Analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , en **Especifique el nombre de usuario o rol que se va a usar al conectarse al modelo**, seleccione **Rol**y, después, en el cuadro de lista desplegable, seleccione **Administrador de ventas por Internet**y haga clic en **Aceptar**.  
  
     Se abrirá Excel con un nuevo libro. Se crea automáticamente una tabla dinámica. La lista de campos de tabla dinámica incluye todos los campos de datos disponibles en su nuevo modelo.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 14: Implementar](lesson-13-deploy.md).  
  
  
