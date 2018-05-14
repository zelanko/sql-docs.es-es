---
title: Cuadro de diálogo Parámetros de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a5b688934e40c8d5d61d46ac500bd9e8c8632afb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Parámetros de la consulta (cuadro de diálogo, Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este cuadro de diálogo permite escribir los valores de los parámetros definidos en la consulta. Este cuadro de diálogo aparece cuando se ejecuta una consulta con parámetros que requieren la entrada de datos por parte del usuario en tiempo de ejecución.  
  
## <a name="options"></a>Opciones  
**Nombre**  
Muestra los parámetros definidos para la consulta que se va a ejecutar. Si la consulta contiene parámetros con nombre, estos nombres aparecerán en la lista. Si la consulta contiene parámetros sin nombre, los nombres de parámetro definidos por el sistema se enumerarán para cada parámetro de la consulta.  
  
**Value**  
Escriba el valor de cada uno de los parámetros mostrados en **Nombre**. El último valor utilizado aparece como valor predeterminado del parámetro.  
  
## <a name="example"></a>Ejemplo  
La consulta siguiente en el panel de SQL abre el cuadro de diálogo Parámetros de la consulta cuando se ejecuta en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] .  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>Ver también  
[Realizar consultas con parámetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
