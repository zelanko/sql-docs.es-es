---
title: Cuadro de diálogo Parámetros de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61707b6ca955ee137cbbc93a6a108dc3930e1b12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63010708"
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Parámetros de la consulta (cuadro de diálogo, Visual Database Tools)
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
 [Realizar consultas con parámetros &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
