---
title: "Ocultar o inmovilizar columnas (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.hideunhidecolumnsdb.f1"
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Ocultar o inmovilizar columnas (SSAS tabular)
  Si en el diseñador de modelos hay columnas que no desea mostrar en una tabla, puede ocultarlas temporalmente. Si oculta una columna, dispone de más espacio en la pantalla para agregar columnas nuevas o para trabajar solo con las columnas de datos pertinentes. Puede ocultar y mostrar columnas desde el menú **Columna** del diseñador de modelos y desde el menú contextual disponible en cada encabezado de columna. Para mantener visible un área de un modelo mientras se desplaza a otra área del modelo, puede inmovilizar columnas específicas para bloquearlas.  
  
> [!IMPORTANT]  
>  La capacidad de ocultar columnas no tiene como finalidad la seguridad de los datos; solo pretende simplificar y acortar la lista de columnas visibles en el diseñador de modelos o en los informes. Para proteger los datos, puede definir roles de seguridad. Los roles solo pueden restringir los metadatos y los datos visibles a los objetos definidos en el rol. Para obtener más información, vea [Roles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
 A la hora de ocultar una columna, tiene la opción de ocultarla mientras trabaja en el diseñador de modelos o en los informes. Si oculta todas las columnas, la tabla aparece vacía en su totalidad en el Diseñador de modelos.  
  
> [!NOTE]  
>  Si necesita ocultar muchas columnas, puede crear una perspectiva en lugar de ocultarlas y mostrarlas. Una perspectiva es una vista personalizada de los datos que facilita el trabajo con subconjuntos de datos relacionados. Para obtener más información, vea [Crear y administrar perspectivas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md).  
  
### Para ocultar una sola columna  
  
1.  En el diseñador de modelos, seleccione la tabla que contenga la columna que desee ocultar.  
  
2.  Haga clic con el botón derecho en la columna, haga clic en **Ocultar columnas** y, después, haga clic en **Desde el Diseñador e Informes**, **Desde informes** o **Desde diseñador**.  
  
### Para ocultar varias columnas  
  
1.  En el diseñador de modelos, seleccione la tabla que contenga las columnas que desee ocultar.  
  
2.  Haga clic en el menú **Columnas** y, a continuación, en **Ocultar y mostrar**.  
  
3.  En el cuadro de diálogo **Ocultar y mostrar columnas** , busque cada columna que desee ocultar y, a continuación, anule la selección de una de las opciones **En diseñador** y **En informes**, o ambas.  
  
4.  Haga clic en **Aceptar**.  
  
### Para inmovilizar columnas  
  
1.  En el diseñador de modelos, seleccione la tabla que contenga las columnas que desee inmovilizar.  
  
2.  Seleccione las columnas que desee inmovilizar.  
  
3.  Haga clic en el menú **Columnas** y, a continuación, en **Inmovilizar**.  
  
    > [!NOTE]  
    >  Cuando se inmovilizan columnas, estas se mueven a la izquierda (o delante) de la tabla en el diseñador. Cuando se libera una columna, esta no recupera su ubicación original.  
  
## Vea también  
 [Definir tablas y columnas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Perspectivas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  