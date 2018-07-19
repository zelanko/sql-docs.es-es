---
title: 'Lección 4: Marcar como tabla de fechas | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77f29250621485f5606a0bf33615e8d15eb7d80b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057813"
---
# <a name="lesson-3-mark-as-date-table"></a>Lección 3: Marcar como tabla de fechas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En la lección 2: Agregar datos, importó una tabla de dimensiones denominada DimDate. Mientras que en el modelo esta tabla se denomina DimDate, también puede ser conocida como un *tabla de fechas*, porque contiene datos de fecha y hora.  
  
Siempre que use funciones de inteligencia de tiempo DAX en los cálculos, como hará al crear medidas un poco más adelante, debe especificar propiedades de tabla de fechas, que incluyen un *tabla de fechas* y un identificador único *fecha columna* en esa tabla.
  
En esta lección, marcará la tabla DimDate como la *tabla de fechas* y la columna de fecha (en la tabla Date) como el *columna de fecha* (identificador único).  

Antes de que se marcan la tabla de fechas y la columna de fecha, necesitamos realizar un pequeño mantenimiento para que sea más fácil comprender nuestro modelo. Observará en la tabla DimDate una columna denominada **FullDateAlternateKey**. Contiene una fila por cada día de cada año de calendario incluido en la tabla. Vamos a usar esta columna mucho en las fórmulas de medida y los informes. Sin embargo, FullDateAlternateKey no es realmente un buen identificador en esta columna. Vamos a cambiar el nombre a **fecha**, lo que sea más fácil identificarlo e incluirlo en fórmulas. Siempre que sea posible, es una buena idea cambiar el nombre de objetos como tablas y columnas para facilitar su identificación en las aplicaciones como Power BI y Excel de informes. 
  
Tiempo estimado para completar esta lección: **3 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 2: agregar datos](../analysis-services/lesson-2-add-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para cambiar el nombre de la columna FullDateAlternateKey

1.  En el Diseñador de modelos, haga clic en el **DimDate** tabla.

2.  Haga doble clic en el encabezado para el **FullDateAlternateKey** columna y, a continuación, cambie su nombre a **fecha**.

  
### <a name="to-set-mark-as-date-table"></a>Para establecer la marca como tabla de fecha  
  
1.  Seleccione la columna **Date** y, en la ventana **Propiedades** , en **Tipo de datos**, asegúrese de que  **Date** está seleccionada.  
  
2.  Haga clic en el menú **Tabla** , haga clic en **Date**y, después, haga clic en **Marcar como tabla de fechas**.  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas** en el cuadro de lista **Date** , seleccione la columna **Date** como identificador único. Normalmente, se seleccionará de forma predeterminada. Haga clic en **Aceptar**. 

    ![como-tabular-lesson3-date-table](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>¿Qué sigue?
Vaya a la siguiente lección: [lección 4: crear relaciones](../analysis-services/lesson-4-create-relationships.md).
  
