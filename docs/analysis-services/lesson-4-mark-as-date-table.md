---
title: "Lecci&#243;n 4: Marcar como tabla de fechas | Microsoft Docs"
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
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 4: Marcar como tabla de fechas
En la Lección 2: Agregar datos, importó una tabla de dimensiones denominada DimDate y cambió el nombre por Date. Aunque en el modelo esta tabla se denomina Date, puede ser también conocida como *tabla Date*, porque contiene datos de fecha y hora.  
  
Siempre que use funciones de Inteligencia de tiempo en los cálculos, como hará al crear medidas más adelante, debe especificar propiedades de tabla de fechas, que incluyen una *tabla Date* y *una columna Date* de identificador único en esa tabla. Puede crear relaciones válidas entre otras tablas y la tabla Date; es necesario para los cálculos con las funciones de inteligencia de tiempo de DAX.  
  
En esta lección, se marcará la tabla Date importada y con el nombre cambiado como *tabla Date* y la columna Date (en la tabla Date) como *columna Date* (identificador único). Todo el uso del nombre Date puede llevar a confusión, pero pronto lo entenderá.  
  
Tiempo estimado para completar esta lección: **3 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 3: Cambiar el nombre de las columnas](../analysis-services/lesson-3-rename-columns.md).  
  
### Para establecer la marca como tabla de fecha  
  
1.  En el diseñador de modelos, haga clic en la tabla **Date** (pestaña).  
  
2.  Seleccione la columna **Date** y, en la ventana **Propiedades**, en **Tipo de datos**, asegúrese de que **Date** está seleccionada.  
  
3.  Haga clic en el menú **Tabla**, haga clic en **Date** y, después, haga clic en **Marcar como tabla de fechas**.  
  
4.  En el cuadro de diálogo **Marcar como tabla de fechas** en el cuadro de lista **Date**, seleccione la columna **Date** como identificador único.  
  
## Pasos siguientes  
Para continuar este tutorial, vaya a la lección siguiente: [Lección 5: Crear relaciones](../analysis-services/lesson-5-create-relationships.md).  
  
  
  
