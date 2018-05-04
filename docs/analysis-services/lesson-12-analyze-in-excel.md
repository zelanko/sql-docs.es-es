---
title: 'Lección 13: Analizar en Excel | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 55e49df3d7e9702ce216952664b0110cd169c3c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-12-analyze-in-excel"></a>Lección 12: Analizar en Excel
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, usará la analizar en función de Excel en SSDT para abrir Microsoft Excel, crear automáticamente una conexión de origen de datos para el área de trabajo del modelo y agregar automáticamente una tabla dinámica a la hoja de cálculo. La característica Analizar en Excel se ha diseñado para proporcionar una manera rápida y sencilla de probar la eficacia del diseño de su modelo antes de implementarlo. No realizará ningún análisis de datos en esta lección. El propósito de esta lección es familiarizar al autor de modelos con las herramientas que puede usar para probar el diseño de sus modelos. A diferencia de la analizar en función de Excel, que está destinado a los autores de modelos, sino que usarán a las aplicaciones de informes, como Excel o Power BI para conectarse y examinar los datos del modelo implementados.  
  
Para completar esta lección, debe tener instalado Excel en el mismo equipo que SSDT. Para obtener más información, consulte [Analizar en Excel](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 11: crear Roles](../analysis-services/lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Examinar utilizando las perspectivas Predeterminada y Venta por Internet  
En estas primeras tareas, examinará su modelo mediante el uso de la perspectiva predeterminada, que incluye todos los objetos del modelo, y también con la perspectiva de ventas por Internet que anteriormente. La perspectiva Venta por Internet excluye el objeto de tabla Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para examinar con la perspectiva predeterminada  
  
1.  Haga clic en el **modelo** menú > **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , haga clic en **Aceptar**.  
  
    Excel se abrirá con un libro nuevo. Se crea una conexión de origen de datos con la cuenta de usuario actual y se utiliza la perspectiva predeterminada para definir los campos visibles. Una tabla dinámica se agrega automáticamente a la hoja de cálculo.  
  
3.  En Excel, en la **lista de campos de tabla dinámica**, tenga en cuenta el **DimDate** y **FactInternetSales** aparecen los grupos de medida, así como el **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, y **FactInternetSales** aparecen las tablas con todos sus respectivas columnas.  
  
4.  Cierre Excel sin guardar el libro.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para examinar con la perspectiva Venta por Internet  
  
1.  Haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , mantenga seleccionado **Usuario de Windows actual** y, después, en el cuadro de lista desplegable **Perspectiva** , seleccione **Venta por Internet**y haga clic en **Aceptar**. 
    
    ![como-tabular-lección 12-perspectiva](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  En Excel, en **PivotTable Fields**, tenga en cuenta la tabla DimCustomer se excluye de la lista de campos.  
    
    ![como-tabular-lección 12-fields](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  Cierre Excel sin guardar el libro.  
  
## <a name="browse-by-using-roles"></a>Examinar mediante roles  
Los roles son una parte integral de cualquier modelo tabular. Sin al menos un rol al que se agregan a los usuarios como miembros, los usuarios no podrán tener acceso y analizar datos con el modelo. La característica Analizar de Excel proporciona una manera de probar los roles que ha definido.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Para examinar mediante el rol de usuario de administrador de ventas  
  
1.  En SSDT, haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En el **analizar en Excel** cuadro de diálogo **especifica el nombre de usuario o rol que se usará para conectarse al modelo**, seleccione **rol**y, a continuación, en el cuadro de lista desplegable, seleccione **Sales Manager**y, a continuación, haga clic en **Aceptar**.  
  
    Excel se abrirá con un libro nuevo. Automáticamente se crea una tabla dinámica. La lista de campos de tabla dinámica incluye todos los campos de datos disponibles en su nuevo modelo.  
      
3.  Cierre Excel sin guardar el libro.  
  
## <a name="whats-next"></a>¿Qué sigue?
Vaya a la siguiente lección: [lección 13: implementar](../analysis-services/lesson-13-deploy.md).

  
  
  
