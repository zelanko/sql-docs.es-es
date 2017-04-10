---
title: "Lecci&#243;n 10: Crear jerarqu&#237;as | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 10: Crear jerarqu&#237;as
En esta lección, creará jerarquías. Las jerarquías son grupos de columnas dispuestas en niveles; por ejemplo, una jerarquía Geografía puede tener subniveles para País, Provincia y Ciudad. Las jerarquías pueden aparecer por separado de otras columnas en una lista de campos de la aplicación cliente de informes, lo que facilita la navegación de los usuarios del cliente y su inclusión en un informe. Para obtener más información, vea [Jerarquías &#40;SSAS tabular&#41;](../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
Para crear jerarquías, usará el diseñador de modelos en *Vista de diagrama*. La creación y administración de jerarquías no se admite en la vista de datos del diseñador de modelos.  
  
Tiempo estimado para completar esta lección: **20 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 9: Crear perspectivas](../Topic/Lesson%209:%20Create%20Perspectives.md).  
  
## Crear jerarquías  
  
#### Para crear una jerarquía Categoría en la tabla Product  
  
1.  En el diseñador de modelos, haga clic en el menú **Modelo**; después, seleccione **Vista de modelo** y haga clic en **Vista de diagrama**.  
  
  
  
2.  Haga clic con el botón derecho en la tabla **Product** y en **Crear jerarquía**. Aparece una nueva jerarquía en la parte inferior de la ventana de tabla.  
  
3.  En el nombre de jerarquía, cambie el nombre escribiendo **Categoría** y, después, presione ENTRAR.  
  
4.  En la tabla **Product**, haga clic en la columna **Product Category Name**, arrástrela hasta la jerarquía **Categoría** y suéltela sobre **Categoría**.  
  
5.  En la jerarquía **Categoría**, haga clic con el botón derecho en la columna **Product Category Name**, haga clic en **Cambiar nombre** y escriba **Categoría**.  
  
    > [!NOTE]  
    > Al cambiar el nombre de una columna de la jerarquía no se cambia el nombre de esa columna en la tabla. Una columna de una jerarquía es simplemente una representación de la columna de la tabla.  
  
6.  En la tabla **Product**, haga clic y arrastre la columna **Product Category Name** hasta la jerarquía **Categoría**.  
  
7.  Cambie el nombre de **Product Subcategory Name** a **Subcategoría**.  
  
8.  Haga clic y arrastre las columnas **Model Name** y **Product Name** (en orden) y colóquelas debajo de la columna **Product Subcategory Name**. Cambie el nombre de estas columnas a **Modelo** y **Producto**, respectivamente.  
  
#### Para crear jerarquías en la tabla Date  
  
1.  En el diseñador de modelos, haga clic con el botón derecho en la tabla **Fecha** y, después, haga clic en **Crear jerarquía**.  
  
2.  Cambie el nombre de la jerarquía a **Calendario**.  
  
3.  Agregue las columnas siguientes, en orden, y después cámbieles el nombre:  
  
    |Columna|Cambiar el nombre a:|  
    |----------|--------------|  
    |Año del calendario|Year|  
    |Semestre del calendario|Semestre|  
    |Trimestre del calendario|Trimestre|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  En la tabla **Fecha**, repita los pasos anteriores y cree una jerarquía **Fiscal** que incluya las siguientes columnas:  
  
    |Columna|Cambiar el nombre a:|  
    |----------|--------------|  
    |Año fiscal|Year|  
    |Semestre fiscal|Semestre|  
    |Trimestre fiscal|Trimestre|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  Finalmente, en la tabla **Fecha**, repita los pasos anteriores y cree una jerarquía **Calendario de producción** que incluya las columnas siguientes:  
  
    |Columna|Cambiar el nombre a:|  
    |----------|--------------|  
    |Año del calendario|Year|  
    |Week Number Of Year|Semana|  
    |Day Of Week|Day|  
  
## Pasos siguientes  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 11: Crear particiones](../analysis-services/lesson-11-create-partitions.md).  
  
  
  
