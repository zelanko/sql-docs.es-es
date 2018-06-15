---
title: 'Lección 4: Marcar como tabla de fechas | Documentos de Microsoft'
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
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019702"
---
# <a name="lesson-3-mark-as-date-table"></a>Lección 3: Marcar como tabla de fechas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

En la lección 2: Agregar datos, importó una tabla de dimensiones denominada DimDate. Mientras que en el modelo de esta tabla se denomina DimDate, también se conoce como un *tabla de fechas*, ya que contiene datos de fecha y hora.  
  
Cada vez que se utilizan funciones de inteligencia de tiempo DAX en los cálculos, tal y como se llevará a cabo al crear medidas un poco más adelante, debe especificar propiedades de tabla de fecha, que incluyen un *tabla de fechas* y un identificador único *fecha columna* de esa tabla.
  
En esta lección, podrá marcar la tabla DimDate como el *tabla de fechas* y la columna de fecha (en la tabla Date) como el *columna de fecha* (identificador único).  

Antes de que se marque la tabla de fechas y la columna de fecha, que necesitamos un poco mantenimiento para hacer que nuestro modelo más fácil de entender. Notará en la tabla DimDate una columna denominada **FullDateAlternateKey**. Contiene una fila para cada día de cada año de calendario incluido en la tabla. Usaremos esta columna mucho en fórmulas de medida y en los informes. Sin embargo, FullDateAlternateKey no es realmente un buen identificador para esta columna. Vamos a cambiar el nombre a **fecha**, lo que sea más fácil identificar e incluir en las fórmulas. Siempre que sea posible, es una buena idea cambiar el nombre de objetos, como tablas y columnas para facilitar su identificación en las aplicaciones como Power BI y Excel de informes. 
  
Tiempo estimado para completar esta lección: **3 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 2: agregar datos](../analysis-services/lesson-2-add-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para cambiar el nombre de la columna FullDateAlternateKey

1.  En el Diseñador de modelos, haga clic en el **DimDate** tabla.

2.  Haga doble clic en el encabezado de la **FullDateAlternateKey** columna y, a continuación, cambie su nombre a **fecha**.

  
### <a name="to-set-mark-as-date-table"></a>Para establecer la marca como tabla de fecha  
  
1.  Seleccione la columna **Date** y, en la ventana **Propiedades** , en **Tipo de datos**, asegúrese de que  **Date** está seleccionada.  
  
2.  Haga clic en el menú **Tabla** , haga clic en **Date**y, después, haga clic en **Marcar como tabla de fechas**.  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas** en el cuadro de lista **Date** , seleccione la columna **Date** como identificador único. Normalmente se seleccionará de forma predeterminada. Haga clic en **Aceptar**. 

    ![como-tabular-lesson3-date-table](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>¿Qué sigue?
Vaya a la siguiente lección: [lección 4: crear relaciones](../analysis-services/lesson-4-create-relationships.md).
  
