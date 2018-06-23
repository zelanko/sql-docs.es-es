---
title: 'Lección 4: Marcar como tabla de fechas | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: a283b56c215e51dbdb0df90b9c51c21e232df2f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109302"
---
# <a name="lesson-4-mark-as-date-table"></a>Lección 4: Marcar como tabla de fechas
  En la lección 2: Agregar datos, importó una tabla de dimensiones denominada DimDate. A continuación cambió el nombre de la tabla DimDate, en la lección 3: Cambiar el nombre de las columnas a, simplemente, Date. Aunque en el modelo esta tabla se denomina Date, puede ser también conocida como *tabla Date*, porque contiene datos de fecha y hora.  
  
 Siempre que use funciones de Inteligencia de tiempo en los cálculos, como hará al crear medidas más adelante, debe especificar propiedades de tabla de fechas, que incluyen una *tabla Date* y *una columna Date* de identificador único en esa tabla. Puede crear relaciones válidas entre otras tablas y la tabla Date; es necesario para los cálculos con las funciones de inteligencia de tiempo de DAX.  
  
 En esta lección, se marcará la tabla Date importada y con el nombre cambiado como *tabla Date* y la columna Date (en la tabla Date) como *columna Date* (identificador único). Todo el uso del nombre Date puede llevar a confusión, pero pronto lo entenderá.  
  
 Tiempo estimado para completar esta lección: **3 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 3: Cambiar el nombre de las columnas](rename-columns.md).  
  
### <a name="to-set-mark-as-date-table"></a>Para establecer la marca como tabla de fecha  
  
1.  En el diseñador de modelos, haga clic en la tabla **Date** (pestaña).  
  
2.  Haga clic en el menú **Tabla**, haga clic en **Date** y, después, haga clic en **Marcar como tabla de fechas**.  
  
3.  En el cuadro de diálogo **Marcar como tabla de fechas** en el cuadro de lista **Date** , seleccione la columna **Date** como identificador único.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para continuar este tutorial, vaya a la lección siguiente: [Lección 5: Crear relaciones](lesson-4-create-relationships.md).  
  
  