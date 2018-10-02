---
title: Cuadro de diálogo Parámetros de la consulta (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.openlocfilehash: f1f530954b2449e3a85822ad04d87cd553ae26a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674179"
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
La consulta siguiente en el panel de SQL abre el cuadro de diálogo Parámetros de la consulta cuando se ejecuta en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>Ver también  
[Realizar consultas con parámetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
