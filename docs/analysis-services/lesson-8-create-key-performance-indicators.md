---
title: "Lecci&#243;n 8: Crear indicadores clave de rendimiento | Microsoft Docs"
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
ms.assetid: a6c8ac2b-64ba-456f-b418-7bf0afe145d1
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 8: Crear indicadores clave de rendimiento
En esta lección, creará indicadores clave de rendimiento (KPI). Los KPI miden el rendimiento de un valor, definido por una medida *base*, con respecto a un valor de *destino*, también definido por una medida o por un valor absoluto. En aplicaciones cliente de informes, los KPI pueden proporcionar a los profesionales del negocio una manera rápida y sencilla de identificar un resumen de logros empresariales o tendencias. Para obtener más información, consulte [KPI &#40;SSAS tabular&#41;](../analysis-services/tabular-models/kpis-ssas-tabular.md).  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 7: Crear medidas](../analysis-services/lesson-7-create-measures.md).  
  
## Crear indicadores clave de rendimiento  
  
#### Para crear un KPI Rendimiento de ventas por Internet del trimestre actual  
  
1.  En el diseñador de modelos, haga clic en la tabla (pestaña) **Ventas por Internet**.  
  
2.  En la cuadrícula de medidas, haga clic en una celda vacía.  
  
3.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula:  
  
    **Rendimiento de ventas por Internet del trimestre actual :=IFERROR([Ventas por Internet del trimestre actual]/[Proporción de ventas por Internet del trimestre anterior hasta la fecha],BLANK())**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
    Esta medida servirá como la medida base del KPI.  
  
4.  En la cuadrícula de medidas, haga clic con el botón derecho en la medida **Rendimiento de ventas por Internet del trimestre actual** y haga clic en **Crear KPI**.  
  
    Se abre el cuadro de diálogo **Indicador clave de rendimiento**.  
  
5.  En el cuadro de diálogo **Indicador clave de rendimiento (KPI)**, en **Destino**, seleccione la opción **Valor absoluto**.  
  
6.  En el campo **Valor absoluto**, escriba **1.1** y pulse ENTRAR.  
  
7.  En el campo de control deslizante situado abajo a la izquierda, escriba **1** y, en el de arriba a la derecha, escriba **1.07**.  
  
8.  En **Seleccionar el estilo de icono**, seleccione el tipo de icono de rombo (rojo), triángulo (amarillo), círculo (verde).  
  
    > [!TIP]  
    > Observe en el campo expansible **Descripciones** los estilos de icono disponibles. Puede especificar descripciones para los distintos elementos de KPI para que sean más fáciles de identificar en las aplicaciones cliente.  
  
9. Haga clic en **Aceptar** para completar el KPI.  
  
    En la cuadrícula de medidas, observe el icono situado junto a la medida **Rendimiento de ventas por Internet del trimestre actual**. Este icono indica que esta medida actúa como valor base de un KPI.  
  
#### Para crear un KPI Rendimiento de margen de ventas por Internet del trimestre actual  
  
1.  En la cuadrícula de medidas de la tabla **Ventas por Internet**, haga clic en una celda vacía.  
  
2.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula:  
  
    **Rendimiento de margen de ventas por Internet del trimestre actual :=IF([Proporción del margen del trimestre anterior de ventas por Internet hasta la fecha]<>0,([Margen del trimestre actual de ventas por Internet]-[Proporción del margen del trimestre anterior de ventas por Internet hasta la fecha])/[Proporción del margen del trimestre anterior de ventas por Internet hasta la fecha],BLANK())**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
3.  En la cuadrícula de medidas, haga clic con el botón derecho en la medida **Rendimiento de margen de ventas por Internet del trimestre actual** y haga clic en **Crear KPI**.  
  
4.  En el cuadro de diálogo **Indicador clave de rendimiento**, en **Definir valor de destino**, seleccione la opción **Valor absoluto**.  
  
5.  En el campo **Valor absoluto**, escriba **1.25**.  
  
6.  En **Definir umbrales de estado**, desplace el campo de control deslizante de abajo a la izquierda hasta que el campo muestre **0.8** y el de arriba a la derecha hasta que muestre **1.03**.  
  
7.  En **Seleccionar estilo de icono**, seleccione el tipo de icono de rombo (rojo), triángulo (amarillo) y círculo (verde), y haga clic en **Aceptar**.  
  
## Paso siguiente  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 9: Crear perspectivas](../Topic/Lesson%209:%20Create%20Perspectives.md).  
  
  
  
