---
title: "Lecci&#243;n 6: Crear columnas calculadas | Microsoft Docs"
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
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lecci&#243;n 6: Crear columnas calculadas
En esta lección creará nuevos datos en el modelo agregando columnas calculadas. Una columna calculada está basada en datos que ya existen en el modelo. Para obtener más información, consulte [Columnas calculadas &#40;SSAS tabular&#41;](../analysis-services/tabular-models/calculated-columns-ssas-tabular.md).  
  
Creará cinco columnas calculadas nuevas en tres tablas diferentes. Los pasos son ligeramente diferentes para cada tarea. Esto es así para mostrarle que hay varias formas de crear nuevas columnas, cambiarles el nombre y colocarlas en distintos lugares de una tabla.  
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 5: Crear relaciones](../analysis-services/lesson-5-create-relationships.md).  
  
## Crear columnas calculadas  
  
#### Crear una columna calculada Calendario del mes en la tabla Date  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo**, elija **Vista de modelo** y, después, haga clic en **Vista de datos**.  
  
    Las columnas calculadas solo se pueden crear mediante el diseñador de modelos en la Vista de datos.  
  
2.  En el diseñador de modelos, haga clic en la tabla **Date** (pestaña).  
  
3.  Haga clic con el botón derecho en el encabezado de la columna **Calendar Quarter** y, después, haga clic en **Insertar columna**.  
  
    Una nueva columna denominada **Columna calculada 1** se inserta a la izquierda de la columna **Calendar Quarter**.  
  
4.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula. Autocompletar sirve de ayuda para escribir los nombres completos de columnas y tablas, y enumera las funciones que están disponibles.  
  
    **=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
    Después, los valores se rellenan para todas las filas de la columna calculada. Si se desplaza hacia abajo por la tabla, verá que las filas pueden tener valores diferentes para esta columna, en función de los datos que haya en cada fila.  
  
    > [!NOTE]  
    > Si aparece un error, compruebe que los nombres de columna de la fórmula coinciden con los nombres de columna que cambió en [Lección 3: Cambiar el nombre de las columnas](../analysis-services/lesson-3-rename-columns.md).  
  
5.  Cambie el nombre de esta columna a **Calendario mensual**.  
  
La columna calculada Calendario del mes proporciona un nombre ordenable del mes.  
  
#### Crear una columna calculada Día de la semana en la tabla Date  
  
1.  Con la tabla **Date** activa, haga clic en el menú **Columna** y luego en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    **=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]**  
  
    Cuando termine de crear la fórmula, presione ENTRAR. Se agrega la columna nueva a la derecha de la tabla.  
  
3.  Cambie el nombre de la columna a **Día de la semana**.  
  
4.  Haga clic en el encabezado de columna y, después, arrastre la columna entre la columna **Day Name** y la columna **Day of Month**.  
  
    > [!TIP]  
    > El movimiento de columnas en la tabla simplifica la navegación.  
  
La columna calculada Día de la semana proporciona un nombre ordenable del día de la semana.  
  
#### Crear una columna calculada Nombre de subcategoría del producto en la tabla Product  
  
1.  En el diseñador de modelos, seleccione la tabla **Product**.  
  
2.  Desplácese hasta el extremo derecho de la tabla. Observe que la columna situada más a la derecha se denomina **Agregar columna** (en cursiva); haga clic en el encabezado de columna.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente.  
  
    **=RELATED('Product Subcategory'[Product Subcategory Name])**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
4.  Cambie el nombre de la columna a **Nombre de subcategoría del producto**.  
  
La columna calculada Nombre de subcategoría del producto se utiliza para crear una jerarquía en la tabla Product que incluya los datos de la columna con igual nombre en la tabla Product Subcategory. Las jerarquías no pueden abarcar más de una tabla. Más adelante, en la lección 7, creará jerarquías.  
  
#### Crear una columna calculada Nombre de categoría del producto en la tabla Product  
  
1.  Con la tabla **Product** activa, haga clic en el menú **Columna** y, después, en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    **=RELATED('Product Category'[Product Category Name])**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
3.  Cambie el nombre de la columna a **Nombre de categoría del producto**.  
  
La columna calculada Nombre de categoría del producto se utiliza para crear una jerarquía en la tabla Product que incluya los datos de la columna con igual nombre en la tabla Product Category. Las jerarquías no pueden abarcar más de una tabla.  
  
#### Crear una columna calculada Margen en la tabla Internet Sales  
  
1.  En el diseñador de modelos, seleccione la tabla **Internet Sales**.  
  
2.  Agregue una nueva columna.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
    **=[Sales Amount]-[Total Product Cost]**  
  
    Cuando termine de crear la fórmula, presione ENTRAR.  
  
4.  Cambie el nombre de la columna a **Margen**.  
  
5.  Arrastre la columna entre la columna **Sales Amount** y la columna **Tax Amt**.  
  
La columna calculada Margen se utiliza para analizar los márgenes de beneficios de cada fila (producto).  
  
## Paso siguiente  
Para continuar esta lección, vaya a la lección siguiente: [Lección 7: Crear medidas](../analysis-services/lesson-7-create-measures.md).  
  
  
  
