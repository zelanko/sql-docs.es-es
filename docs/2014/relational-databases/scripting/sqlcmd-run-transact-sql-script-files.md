---
title: Ejecutar archivos de scripts Transact-SQL mediante sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dd52c6fb0c5533450a7e32ad68a156406873fdb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136252"
---
# <a name="run-transact-sql-script-files-using-sqlcmd"></a>Ejecutar archivos de scripts Transact-SQL mediante sqlcmd
  Puede utilizar `sqlcmd` para ejecutar un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] es un archivo de texto que puede incluir una combinación de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], comandos `sqlcmd` y variables de scripting.  
  
 Para crear un archivo sencillo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante el Bloc de notas, siga estos pasos:  
  
1.  Haga clic en **Inicio**, seleccione **Todos los programas**, **Accesorios**y, a continuación, haga clic en **Bloc de notas**.  
  
2.  Copie y pegue el siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)] en el Bloc de notas:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT p.FirstName + ' ' + p.LastName AS 'Employee Name',  
    a.AddressLine1, a.AddressLine2 , a.City, a.PostalCode   
    FROM Person.Person AS p   
       INNER JOIN HumanResources.Employee AS e   
            ON p.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.BusinessEntityAddress bea   
            ON bea.BusinessEntityID = e.BusinessEntityID  
        INNER JOIN Person.Address AS a   
            ON a.AddressID = bea.AddressID;  
    GO  
    ```  
  
3.  Guarde el archivo como **myScript.sql** en la unidad C.  
  
### <a name="to-run-the-script-file"></a>Para ejecutar el archivo de script  
  
1.  Abra una ventana del símbolo del sistema.  
  
2.  En la ventana de símbolo del sistema, escriba: `sqlcmd -S myServer\instanceName -i C:\myScript.sql`  
  
3.  Presione ENTRAR.  
  
 En la ventana del símbolo del sistema se escribe una lista con las direcciones y los nombres de los empleados que figuran en [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] .  
  
### <a name="to-save-this-output-to-a-text-file"></a>Para guardar los resultados en un archivo de texto  
  
1.  Abra una ventana del símbolo del sistema.  
  
2.  En la ventana de símbolo del sistema, escriba: `sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt`  
  
3.  Presione ENTRAR.  
  
 La ventana del símbolo del sistema no devuelve resultados. En su lugar, los resultados se envían al archivo EmpAdds.txt. Para comprobar los resultados, abra el archivo EmpAdds.txt.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar la utilidad sqlcmd](sqlcmd-start-the-utility.md)   
 [sqlcmd (utilidad)](../../tools/sqlcmd-utility.md)  
  
  
