---
title: Cuadro de diálogo Parámetros de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c3e99a38d3b9c06257f4f5202a3142292409d29e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113281"
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>Parámetros de la consulta (cuadro de diálogo, Visual Database Tools)
  Este cuadro de diálogo permite escribir los valores de los parámetros definidos en la consulta. Este cuadro de diálogo aparece cuando se ejecuta una consulta con parámetros que requieren la entrada de datos por parte del usuario en tiempo de ejecución.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Muestra los parámetros definidos para la consulta que se va a ejecutar. Si la consulta contiene parámetros con nombre, estos nombres aparecerán en la lista. Si la consulta contiene parámetros sin nombre, los nombres de parámetro definidos por el sistema se enumerarán para cada parámetro de la consulta.  
  
 **Value**  
 Escriba el valor de cada uno de los parámetros mostrados en **Nombre**. El último valor utilizado aparece como valor predeterminado del parámetro.  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente en el panel de SQL abre el cuadro de diálogo Parámetros de la consulta cuando se ejecuta en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>Vea también  
 [Realizar consultas con parámetros &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  