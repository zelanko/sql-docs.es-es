---
title: Comprobar consultas (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e2aa0172a18bb1b01297caa9dcf4db07888ce083
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="verify-queries-visual-database-tools"></a>Comprobar consultas (Visual Database Tools)
Para evitar problemas, puede comprobar la consulta generada con el fin de asegurarse de que su sintaxis es correcta. Esta opción será especialmente útil cuando escriba instrucciones en el [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
Conviene tener en cuenta estos aspectos a la hora de comprobar las consultas:  
  
-   Una instrucción puede ser válida y, por tanto, comprobarse correctamente, aunque no se pueda representar en el **panel Diagrama** ni en el **panel Criterios**.  
  
-   La comprobación del código SQL puede detectar algunos errores de sintaxis SQL, pero no todos. Si una consulta contiene un error no detectado durante la comprobación SQL, la base de datos detectará el error cuando ejecute la consulta.  
  
-   Las consultas que contienen parámetros no pueden comprobarse.  
  
### <a name="to-verify-an-sql-statement"></a>Para comprobar una instrucción SQL  
  
-   Haga clic con el botón derecho en el **panel SQL**y seleccione **Comprobar sintaxis SQL** en el menú contextual.  
  
## <a name="see-also"></a>Vea también  
[Ejecutar consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Realizar operaciones básicas con consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

