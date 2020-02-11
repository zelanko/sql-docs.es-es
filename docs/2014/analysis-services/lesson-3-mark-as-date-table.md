---
title: 'Lección 4: marcar como tabla de fechas | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26877c4892b050cbf9c8dcc6553530dff513f8fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078784"
---
# <a name="lesson-4-mark-as-date-table"></a>Lección 4: Marcar como tabla de fechas
  En la lección 2: Agregar datos, importó una tabla de dimensiones denominada DimDate. A continuación cambió el nombre de la tabla DimDate, en la lección 3: Cambiar el nombre de las columnas a, simplemente, Date. Aunque en el modelo esta tabla se denomina Date, puede ser también conocida como *tabla Date*, porque contiene datos de fecha y hora.  
  
 Siempre que use funciones de Inteligencia de tiempo en los cálculos, como hará al crear medidas más adelante, debe especificar propiedades de tabla de fechas, que incluyen una *tabla Date* y *una columna Date* de identificador único en esa tabla. Puede crear relaciones válidas entre otras tablas y la tabla Date; es necesario para los cálculos con las funciones de inteligencia de tiempo de DAX.  
  
 En esta lección, se marcará la tabla Date importada y con el nombre cambiado como *tabla Date* y la columna Date (en la tabla Date) como *columna Date* (identificador único). Todo el uso del nombre Date puede ser confuso, pero pronto obtendrá la idea.  
  
 Tiempo estimado para completar esta lección: **3 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 3: Cambiar el nombre de las columnas](rename-columns.md).  
  
### <a name="to-set-mark-as-date-table"></a>Para establecer Marcar como tabla de fechas, siga estos pasos:  
  
1.  En el diseñador de modelos, haga clic en la tabla **Date** (pestaña).  
  
2.  Haga clic en el menú **Tabla**, haga clic en **Fecha** y luego en **Marcar como tabla de fechas**.  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas**, en el cuadro de lista **Fecha**, seleccione la columna **Date** como identificador único.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 5: Crear relaciones](lesson-4-create-relationships.md).  
  
  
