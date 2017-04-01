---
title: "Lecci&#243;n 9: Crear perspectivas | Microsoft Docs"
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
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 9: Crear perspectivas
En esta lección, creará una perspectiva Venta por Internet. Una perspectiva define un subconjunto visible de un modelo que ofrece puntos de vista centrados, específicos del negocio o específicos de la aplicación. Cuando un usuario se conecta a un modelo utilizando una perspectiva, solo ve los objetos del modelo (tablas, columnas, medidas, jerarquías y KPI) como campos definidos en esa perspectiva.  
  
La perspectiva Venta por Internet que va a crear en esta lección excluirá el objeto de tabla Cliente. Al crear una perspectiva que excluye ciertos objetos en la vista, ese objeto todavía existe en el modelo; sin embargo, no está visible en una lista de campos del cliente de informe. Las columnas calculadas y medidas se pueden incluir en una perspectiva o no pueden calcularse a partir de los datos del objeto excluido.  
  
El propósito de esta lección es describir cómo se crean las perspectivas y permitir que se familiarice con las herramientas de creación de modelos tabulares. Si posteriormente amplía el modelo para incluir tablas adicionales, puede crear otras perspectivas para definir puntos de vista diferentes del modelo, como Inventario y Personal de ventas.  
  
Para obtener más información, consulte [Perspectivas &#40;SSAS tabular&#41;](../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **5 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 8: Crear indicadores clave de rendimiento](../analysis-services/lesson-8-create-key-performance-indicators.md).  
  
## Crear perspectivas  
  
#### Para crear una perspectiva Venta por Internet  
  
1.  En el diseñador de modelos, haga clic en el menú **Modelo**, haga clic en **Perspectivas** y, después, en **Crear y administrar**.  
  
2.  En el cuadro de diálogo **Perspectivas**, haga clic en **Nueva perspectiva**.  
  
3.  Para cambiar el nombre de la perspectiva, haga doble clic en el encabezado de columna **Nueva perspectiva 1** y, después, escriba **Ventas por Internet**.  
  
4.  En **Campos**, seleccione las tablas siguientes: **Fecha**, **Geografía**, **Producto**, **Categoría del producto**, **Subcategoría del producto** y **Ventas por Internet**.  
  
    Tenga en cuenta que excluyó la tabla Cliente y todas sus columnas de esta perspectiva. Más adelante, en la lección 12, utilizará la característica Analizar en Excel para probar esta perspectiva. La lista de campos de tabla dinámica de Excel incluirá todas las tablas, excepto la tabla Cliente.  
  
5.  Compruebe sus selecciones, asegúrese de que no está marcada la tabla **Cliente** y, después, haga clic en **Aceptar**  
  
## Pasos siguientes  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 10: Crear jerarquías](../analysis-services/lesson-10-create-hierarchies.md).  
  
  
  
