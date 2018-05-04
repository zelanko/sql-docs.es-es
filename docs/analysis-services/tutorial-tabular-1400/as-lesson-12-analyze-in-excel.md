---
title: 'Lección tutorial de Analysis Services 12: analizar en Excel | Documentos de Microsoft'
description: Describe cómo utilizar analizar en Excel en el proyecto de tutorial de Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 6e6c4ed1eb92a629a8916bd1eae455b82914ae0c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="analyze-in-excel"></a>Analizar en Excel

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, usa la característica analizar en Excel para abrir Microsoft Excel, crear automáticamente una conexión en el área de trabajo del modelo y agregar automáticamente una tabla dinámica a la hoja de cálculo. La característica Analizar en Excel se ha diseñado para proporcionar una manera rápida y sencilla de probar la eficacia del diseño de su modelo antes de implementarlo. No realice ningún análisis de datos en esta lección. El propósito de esta lección es familiarizar al autor de modelos con las herramientas que puede usar para probar el diseño de sus modelos.   
  
Para completar esta lección, debe tener instalado Excel en el mismo equipo que Visual Studio.
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 11: crear roles](../tutorial-tabular-1400/as-lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Examinar utilizando las perspectivas Predeterminada y Venta por Internet  

En estas primeras tareas, examinar el modelo mediante el uso de la perspectiva predeterminada, que incluye todos los objetos del modelo, y también con la perspectiva de ventas por Internet que anteriormente. La perspectiva Venta por Internet excluye el objeto de tabla Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para examinar con la perspectiva predeterminada  
  
1.  Haga clic en el **modelo** menú > **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , haga clic en **Aceptar**.  
  
    Excel se abre con un nuevo libro. Se crea una conexión de origen de datos con la cuenta de usuario actual y se utiliza la perspectiva predeterminada para definir los campos visibles. Una tabla dinámica se agrega automáticamente a la hoja de cálculo.  
  
3.  En Excel, en la **lista de campos de tabla dinámica**, tenga en cuenta el **DimDate** y **FactInternetSales** aparecen los grupos de medida. El **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, y **FactInternetSales** también aparezcan las tablas con sus respectivas columnas.  
  
4.  Cierre Excel sin guardar el libro.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para examinar con la perspectiva Venta por Internet  
  
1.  Haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , mantenga seleccionado **Usuario de Windows actual** y, después, en el cuadro de lista desplegable **Perspectiva** , seleccione **Venta por Internet**y haga clic en **Aceptar**. 
    
    ![perspectiva como lección 12](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  En Excel, en **PivotTable Fields**, tenga en cuenta la tabla DimCustomer se excluye de la lista de campos.  
    
    ![campos como lección 12](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  Cierre Excel sin guardar el libro.  
  
## <a name="browse-by-using-roles"></a>Examinar mediante roles  

Las funciones son una parte importante de cualquier modelo tabular. Sin al menos un rol al que se agregan a los usuarios como miembros, los usuarios no se pueden tener acceso a y analizar datos con el modelo. La característica Analizar de Excel proporciona una manera de probar los roles que ha definido.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Para examinar mediante el rol de usuario de administrador de ventas  
  
1.  En SSDT, haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En **especifica el nombre de usuario o rol que se usará para conectarse al modelo**, seleccione **rol**y, a continuación, en el cuadro de lista desplegable, seleccione **Sales Manager**y, a continuación, haga clic en **Aceptar**.  
  
    Excel se abre con un nuevo libro. Automáticamente se crea una tabla dinámica. La lista de campos de tabla dinámica incluye todos los campos de datos disponibles en el nuevo modelo.  
      
3.  Cierre Excel sin guardar el libro.  
  
## <a name="whats-next"></a>¿Qué sigue?

Vaya a la siguiente lección: [lección 13: implementar](../tutorial-tabular-1400/as-lesson-13-deploy.md).

  
  
  
