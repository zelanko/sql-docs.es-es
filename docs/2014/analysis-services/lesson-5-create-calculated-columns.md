---
title: 'Lección 6: Crear columnas calculadas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58ba761f3e32f13ddcf81dc9875057195298c705
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078558"
---
# <a name="lesson-6-create-calculated-columns"></a>Lección 6: Crear columnas calculadas
  En esta lección creará nuevos datos en el modelo agregando columnas calculadas. Una columna calculada está basada en datos que ya existen en el modelo. Para obtener más información, consulte [Columnas calculadas &#40;SSAS tabular&#41;](tabular-models/ssas-calculated-columns.md).  
  
 Creará cinco columnas calculadas nuevas en tres tablas diferentes. Los pasos son ligeramente diferentes para cada tarea. Esto es así para mostrarle que hay varias formas de crear nuevas columnas, cambiarles el nombre y colocarlas en distintos lugares de una tabla.  
  
 Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 5: Crear relaciones](lesson-4-create-relationships.md).  
  
## <a name="create-calculated-columns"></a>Crear columnas calculadas  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Crear una columna calculada Calendario del mes en la tabla Date  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Modelo**, elija **Vista de modelo** y, después, haga clic en **Vista de datos**.  
  
     Las columnas calculadas solo se pueden crear mediante el diseñador de modelos en la Vista de datos.  
  
2.  En el diseñador de modelos, haga clic en la tabla **Date** (pestaña).  
  
3.  Haga clic en el **Calendar Quarter** columna y, a continuación, haga clic en **Insertar columna**.  
  
     Una nueva columna denominada **CalculatedColumn1** se inserta a la izquierda de la **Calendar Quarter** columna.  
  
4.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula. Autocompletar sirve de ayuda para escribir los nombres completos de columnas y tablas, y enumera las funciones que están disponibles.  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
     Después, los valores se rellenan para todas las filas de la columna calculada. Si se desplaza hacia abajo por la tabla, verá que las filas pueden tener valores diferentes para esta columna, en función de los datos que haya en cada fila.  
  
    > [!NOTE]  
    >  Si recibe un error, compruebe los nombres de columna en la fórmula coinciden con los nombres de columna que cambió en [lección 3: Cambiar el nombre de las columnas](rename-columns.md).  
  
5.  Cambiar el nombre de esta columna a `Month Calendar`.  
  
 La columna calculada Calendario del mes proporciona un nombre ordenable del mes.  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Crear una columna calculada Día de la semana en la tabla Date  
  
1.  Con la tabla **Date** activa, haga clic en el menú **Columna** y luego en **Agregar columna**.  
  
     Se agrega una columna nueva a la derecha de la tabla.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
3.  Cambiar el nombre de la columna a `Day of Week`.  
  
4.  Haga clic en el encabezado de columna y, después, arrastre la columna entre la columna **Day Name** y la columna **Day of Month** .  
  
    > [!TIP]  
    >  El movimiento de columnas en la tabla simplifica la navegación.  
  
 La columna calculada Día de la semana proporciona un nombre ordenable del día de la semana.  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Crear una columna calculada Nombre de subcategoría del producto en la tabla Product  
  
1.  En el diseñador de modelos, seleccione la tabla **Product** .  
  
2.  Desplácese hasta el extremo derecho de la tabla. Observe que la columna situada más a la derecha se denomina **Agregar columna** (en cursiva); haga clic en el encabezado de columna.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente.  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
4.  Cambiar el nombre de la columna a `Product Subcategory Name`.  
  
 La columna calculada Nombre de subcategoría del producto se utiliza para crear una jerarquía en la tabla Product que incluya los datos de la columna con igual nombre en la tabla Product Subcategory. Las jerarquías no pueden abarcar más de una tabla. Más adelante, en la lección 7, creará jerarquías.  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Crear una columna calculada Nombre de categoría del producto en la tabla Product  
  
1.  Con la tabla **Product** activa, haga clic en el menú **Columna** y, después, en **Agregar columna**.  
  
2.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
3.  Cambiar el nombre de la columna a `Product Category Name`.  
  
 La columna calculada Nombre de categoría del producto se utiliza para crear una jerarquía en la tabla Product que incluya los datos de la columna con igual nombre en la tabla Product Category. Las jerarquías no pueden abarcar más de una tabla.  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Crear una columna calculada Margen en la tabla Internet Sales  
  
1.  En el diseñador de modelos, seleccione la tabla **Internet Sales** .  
  
2.  Agregue una nueva columna.  
  
3.  En la barra de fórmulas, escriba la fórmula siguiente:  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     Cuando termine de crear la fórmula, presione ENTRAR.  
  
4.  Cambiar el nombre de la columna a `Margin`.  
  
5.  Arrastre la columna entre la columna **Sales Amount** y la columna **Tax Amt** .  
  
 La columna calculada Margen se utiliza para analizar los márgenes de beneficios de cada fila (producto).  
  
## <a name="next-step"></a>Paso siguiente  
 Para continuar esta lección, vaya a la lección siguiente: [Lección 7: Crear medidas](lesson-6-create-measures.md).  
  
  
