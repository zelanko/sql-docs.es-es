---
title: Cuadro de diálogo Parámetros de consulta
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 05e99d2fc2365ab39b68ad6211889047a1564113
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255367"
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Parámetros de la consulta (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este cuadro de diálogo permite escribir los valores de los parámetros definidos en la consulta. Este cuadro de diálogo aparece cuando se ejecuta una consulta con parámetros que requieren la entrada de datos por parte del usuario en tiempo de ejecución.  
  
## <a name="options"></a>Opciones  
**Nombre**  
Muestra los parámetros definidos para la consulta que se va a ejecutar. Si la consulta contiene parámetros con nombre, estos nombres aparecerán en la lista. Si la consulta contiene parámetros sin nombre, los nombres de parámetro definidos por el sistema se enumerarán para cada parámetro de la consulta.  
  
**Valor**  
Escriba el valor de cada uno de los parámetros mostrados en **Nombre**. El último valor utilizado aparece como valor predeterminado del parámetro.  
  
## <a name="example"></a>Ejemplo  
La consulta siguiente en el panel de SQL abre el cuadro de diálogo Parámetros de la consulta cuando se ejecuta en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>Consulte también  
[Realizar consultas con parámetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
