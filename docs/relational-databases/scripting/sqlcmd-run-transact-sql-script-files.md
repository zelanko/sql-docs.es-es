---
title: Ejecutar archivos de scripts Transact-SQL mediante sqlcmd | Microsoft Docs
ms.custom: 
ms.date: 07/15/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transact sql scripts
ms.assetid: 90067eb8-ca3e-44e8-bb1a-bf7d1a359423
caps.latest.revision: 
author: mightypen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 815b9a2deb8dd4c3f81e46257ae3756eeefe9512
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcmd---run-transact-sql-script-files"></a>sqlcmd - Ejecutar archivos de scripts Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Use **sqlcmd** para ejecutar un archivo de script de Transact-SQL. Un archivo de script de Transact-SQL es un archivo de texto que puede incluir una combinación de instrucciones Transact-SQL, comandos **sqlcmd** y variables de scripting.  

## <a name="create-a-script-file"></a>Crear un archivo de script  
 Para crear un archivo sencillo de script de Transact-SQL mediante el Bloc de notas, siga estos pasos:  
  
1.  Haga clic en **Inicio**, seleccione **Todos los programas**, **Accesorios**y, a continuación, haga clic en **Bloc de notas**.  
  
2.  Copie y pegue el siguiente código Transact-SQL en el Bloc de notas:  
  
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
  
## <a name="run-the-script-file"></a>Ejecutar el archivo de script  
  
1.  Abra una ventana del símbolo del sistema.  
  
2.  En la ventana de símbolo del sistema, escriba: **sqlcmd -S myServer\instanceName -i C:\myScript.sql**.  
  
3.  Presione ENTRAR.  
  
 En la ventana del símbolo del sistema se escribe una lista con las direcciones y los nombres de los empleados que figuran en [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] .  

## <a name="save-the-output-to-a-text-file"></a>Guardar los resultados en un archivo de texto
  
1.  Abra una ventana del símbolo del sistema.  
  
2.  En la ventana de símbolo del sistema, escriba: **sqlcmd -S myServer\instanceName -i C:\myScript.sql -o C:\EmpAdds.txt**.  
  
3.  Presione ENTRAR.  
  
 La ventana del símbolo del sistema no devuelve resultados. En su lugar, los resultados se envían al archivo EmpAdds.txt. Para comprobar los resultados, abra el archivo EmpAdds.txt.  
  
## <a name="see-also"></a>Ver también  
 [Iniciar la utilidad sqlcmd](../../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)  
  
  
