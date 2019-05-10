---
title: 'Lección 12: Analizar en Excel | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8a558dafb4619ef9c4d66884f1fea9fd98e0881c
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404107"
---
# <a name="lesson-12-analyze-in-excel"></a>Lección 12: Analizar en Excel
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

En esta lección, usará la analizar en función de Excel en SSDT al abrir Microsoft Excel, crear automáticamente una conexión de origen de datos para el área de trabajo del modelo y agregar automáticamente una tabla dinámica a la hoja de cálculo. La característica Analizar en Excel se ha diseñado para proporcionar una manera rápida y sencilla de probar la eficacia del diseño de su modelo antes de implementarlo. No realizará ningún análisis de datos en esta lección. El propósito de esta lección es familiarizar al autor de modelos con las herramientas que puede usar para probar el diseño de sus modelos. A diferencia de utilizar el analizar en función de Excel, que está destinada a los autores de modelos, los usuarios finales usará a las aplicaciones de informes, como Excel o Power BI para conectarse y examinar los datos del modelo implementados.  
  
Para completar esta lección, Excel debe instalarse en el mismo equipo que SSDT. Para obtener más información, consulte [Analizar en Excel](../tabular-models/analyze-in-excel-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 11: Crear Roles](lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Examinar utilizando las perspectivas Predeterminada y Venta por Internet  
En estas primeras tareas, examinará su modelo mediante el uso de ambos la perspectiva predeterminada, que incluye todos los objetos del modelo, y también mediante el uso de la perspectiva venta por Internet que anteriormente. La perspectiva Venta por Internet excluye el objeto de tabla Cliente.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>Para examinar con la perspectiva predeterminada  
  
1.  Haga clic en el **modelo** menú > **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , haga clic en **Aceptar**.  
  
    Excel se abrirá con un libro nuevo. Se crea una conexión de origen de datos con la cuenta de usuario actual y se utiliza la perspectiva predeterminada para definir los campos visibles. Una tabla dinámica se agrega automáticamente a la hoja de cálculo.  
  
3.  En Excel, en el **lista de campos de tabla dinámica**, tenga en cuenta la **DimDate** y **FactInternetSales** aparecen los grupos de medida, así como el **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, y **FactInternetSales** aparecen las tablas con todas sus columnas respectivas.  
  
4.  Cierre Excel sin guardar el libro.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Para examinar con la perspectiva Venta por Internet  
  
1.  Haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , mantenga seleccionado **Usuario de Windows actual** y, después, en el cuadro de lista desplegable **Perspectiva** , seleccione **Venta por Internet**y haga clic en **Aceptar**. 
    
    ![as-tabular-lesson12-perspective](media/as-tabular-lesson12-perspective.png)
    
3.  En Excel, en **PivotTable Fields**, tenga en cuenta la tabla DimCustomer se excluye de la lista de campos.  
    
    ![as-tabular-lesson12-fields](media/as-tabular-lesson12-fields.png)
    
4.  Cierre Excel sin guardar el libro.  
  
## <a name="browse-by-using-roles"></a>Examinar mediante roles  
Los roles son una parte integral de cualquier modelo tabular. Sin al menos un rol al que se agregan usuarios como miembros, los usuarios no podrán obtener acceso a análisis de datos mediante el modelo. La característica Analizar de Excel proporciona una manera de probar los roles que ha definido.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Para examinar mediante el rol de usuario director de ventas  
  
1.  En SSDT, haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En el **analizar en Excel** cuadro de diálogo **especifique el nombre de usuario o rol que se usará para conectarse al modelo**, seleccione **rol**y, a continuación, en el cuadro de lista desplegable, seleccione **Jefe de ventas**y, a continuación, haga clic en **Aceptar**.  
  
    Excel se abrirá con un libro nuevo. Automáticamente se crea una tabla dinámica. La lista de campos de tabla dinámica incluye todos los campos de datos disponibles en su nuevo modelo.  
      
3.  Cierre Excel sin guardar el libro.  
  
## <a name="whats-next"></a>¿Qué sigue?
Vaya a la lección siguiente: [Lección 13: Implementar](lesson-13-deploy.md).

  
  
  
