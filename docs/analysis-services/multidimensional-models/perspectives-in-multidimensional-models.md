---
title: "Perspectivas de modelos multidimensionales | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "miembros predeterminados"
  - "ocultar objetos de perspectiva"
  - "perspectivas, cambiar nombre"
  - "atributos [Analysis Services], miembros predeterminados"
  - "perspectivas, quitar"
  - "perspectivas [Analysis Services]"
  - "nombres [Analysis Services], perspectivas"
  - "cubos [Analysis Services], perspectivas"
  - "perspectivas, eliminar"
ms.assetid: 5a3d6577-6833-4c24-820c-b65bb856157b
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Perspectivas de modelos multidimensionales
  Una perspectiva es un subconjunto de un cubo creado para una aplicación o grupo de usuarios específico. El cubo es la perspectiva predeterminada. Una perspectiva se muestra al cliente como un cubo. Cuando el usuario ve una perspectiva, se muestra como otro cubo. Los cambios realizados en los datos del cubo mediante la reescritura en la perspectiva se realizan en el cubo original. Para obtener más información sobre las vistas de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Perspectivas](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md).  
  
 Puede usar la pestaña **Perspectivas** del Diseñador de cubos para crear y modificar las perspectivas de un cubo. La primera columna de la pestaña **Perspectivas** es la columna **Objetos de cubo** , que muestra todos los objetos del cubo. Se corresponde con la perspectiva predeterminada del cubo, que es el propio cubo.  
  
## Crear o eliminar perspectivas  
 Para agregar una perspectiva a la pestaña **Perspectivas** , haga clic en **Nueva perspectiva** en el menú **Cubo** . También puede hacer clic en el botón **Nueva perspectiva** de la barra de herramientas o hacer clic con el botón derecho en el panel y hacer clic en **Nueva perspectiva** en el menú contextual. Puede agregar cualquier cantidad de perspectivas al cubo.  
  
 Para quitar una perspectiva, haga clic en una celda de la columna de la perspectiva que desee eliminar. A continuación, en el menú **Cubo** , haga clic en **Eliminar perspectiva**. También puede hacer clic en el botón **Eliminar perspectiva** en la barra de herramientas, o bien hacer clic con el botón derecho en la perspectiva que quiera eliminar y, después, hacer clic en **Eliminar perspectiva** en el menú contextual.  
  
## Cambiar el nombre de perspectivas  
 La primera fila de cada perspectiva muestra el nombre. Al crear una perspectiva, el nombre inicial es Perspectiva (seguido de un número ordinal, comenzando por 1, si ya existiese una perspectiva denominada Perspectiva). Para editar el nombre de una perspectiva, haga clic en el nombre.  
  
## Ocultar objetos de una perspectiva  
 Para ocultar un objeto de una perspectiva, desactive la casilla de la fila correspondiente al objeto de la columna de la perspectiva. Entre los objetos del cubo que pueden ocultarse de una perspectiva se encuentran:  
  
-   Grupos de medida  
  
-   medidas  
  
-   Dimensions  
  
-   Jerarquías  
  
-   Conjuntos con nombre  
  
-   KPI  
  
-   Acciones  
  
-   Miembros calculados  
  
 Para ver un objeto, expanda la categoría (**Grupos de medida**, **Dimensiones**, **KPI**, **Cálculos** o **Acciones**) para cualquier tipo de objeto en **Objetos de cubo**. Para ver las jerarquías o los atributos de una dimensión, expanda primero una dimensión y, a continuación, la fila **Jerarquías** o **Atributos** . Para ver las medidas de un grupo de medida, expanda el grupo de medida.  
  
## Vea también  
 [Cubos en modelos multidimensionales](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  