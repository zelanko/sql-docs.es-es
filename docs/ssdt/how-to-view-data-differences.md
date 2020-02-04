---
title: Consulta de las diferencias de los datos
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.f1
ms.assetid: f88d3350-2eaf-44cc-96a8-84008b6cd071
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 5c9e80f6289ff3313a3eeb7cec0601fb2c651aa2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75226751"
---
# <a name="how-to-view-data-differences"></a>Cómo: Ver diferencias de datos

Después de comparar los datos de dos bases de datos, verá cada uno de los *objetos de base de datos* comparado y su estado. También puede ver los resultados de los registros dentro de cada objeto, agrupados por estado.  
  
Una vez haya visto las diferencias, puede actualizar el *destino* para que coincida con el *origen* de algunos o todos los objetos o registros que son diferentes, faltan o son nuevos.  
  
### <a name="to-view-data-differences"></a>Para ver las diferencias de los datos  
  
1.  Compare los datos de un origen y un destino.  
  
2.  (Opcional) Realice una o ambas de las acciones siguientes:  
  
    -   De forma predeterminada, los resultados de todos los objetos aparecen, independientemente de su estado. Para mostrar solo los objetos que tienen un estado determinado, haga clic en una opción de la lista **Filtro**.  
  
    -   Para ver los resultados de los registros de un objeto determinado, haga clic en el objeto en el panel de resultados principal y, a continuación, haga clic en una ficha en el panel de vista de registros. Cada pestaña muestra todos los registros en ese objeto que tienen un estado específico: diferente, solo en origen, solo en destino e idénticos. Los datos aparecen en el registro y la columna.  
  
## <a name="see-also"></a>Consulte también  
[Cómo: Usar Comparación de esquemas para comparar distintas definiciones de base de datos](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
