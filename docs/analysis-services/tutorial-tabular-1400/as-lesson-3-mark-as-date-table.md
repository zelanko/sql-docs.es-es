---
title: 'Analysis Services lección del tutorial 3: Marcar como tabla de fechas | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2008f066d537b1f88b9bf674c4a864217eae9890
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685576"
---
# <a name="mark-as-date-table"></a>Marcar como tabla de fechas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En la lección 2: Obtener datos, importó una tabla de dimensiones denominada **DimDate**. Mientras que en el modelo esta tabla se denomina DimDate, también puede ser conocida como un *tabla de fechas*, porque contiene datos de fecha y hora.  
  
Siempre que use las funciones de inteligencia de tiempo DAX, como al crear medidas más adelante, debe especificar las propiedades que incluyen un *tabla de fechas* y un identificador único *columna de fecha* en esa tabla.
  
En esta lección, se marca el **DimDate** tabla como el *tabla de fechas* y **fecha** columna (en la tabla Date) como el *columna de fecha* (único identificador).  

Antes de marcar la tabla de fechas y la columna de fecha, es un buen momento para realizar un pequeño mantenimiento para que su modelo sea más fácil de entender. Tenga en cuenta en la tabla DimDate una columna denominada **FullDateAlternateKey**. Esta columna contiene una fila por cada día de cada año de calendario incluido en la tabla. Utilice esta columna mucho en las fórmulas de medida y los informes. Sin embargo, FullDateAlternateKey no es realmente un buen identificador en esta columna. Cambiar el nombre a **fecha**, lo que sea más fácil identificarlo e incluirlo en fórmulas. Siempre que sea posible, es una buena idea cambiar el nombre de objetos como tablas y columnas para que sean fáciles de identificar en SSDT y las aplicaciones de informes. 
  
Tiempo estimado para completar esta lección: **Tres minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 2: Obtener datos](../tutorial-tabular-1400/as-lesson-2-get-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Para cambiar el nombre de la columna FullDateAlternateKey

1.  En el Diseñador de modelos, haga clic en el **DimDate** tabla.

2.  Haga doble clic en el encabezado para el **FullDateAlternateKey** columna y, a continuación, cambie su nombre a **fecha**.

  
### <a name="to-set-mark-as-date-table"></a>Para establecer la marca como tabla de fecha  
  
1.  Seleccione la columna **Date** y, en la ventana **Propiedades** , en **Tipo de datos**, asegúrese de que  **Date** está seleccionada.  
  
2.  Haga clic en el menú **Tabla** , haga clic en **Date**y, después, haga clic en **Marcar como tabla de fechas**.  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas** en el cuadro de lista **Date** , seleccione la columna **Date** como identificador único. Normalmente se selecciona de forma predeterminada. Haga clic en **Aceptar**. 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>¿Qué sigue?

[Lección 4: Crear relaciones](../tutorial-tabular-1400/as-lesson-4-create-relationships.md).
  
