---
title: Solución de problemas con las pruebas unitarias de base de datos en SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf4c9cd1-7e73-4c3b-922a-68b9247e7b33
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 132796555d806e14b6d234726b742943915c34d2
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094765"
---
# <a name="troubleshooting-sql-server-database-unit-testing-issues"></a>Solucionar problemas con las pruebas unitarias de base de datos en SQL Server
Es posible que se produzcan los problemas que se describen en este tema cuando trabaje con pruebas unitarias de SQL Server en una base de datos:  
  
-   [Se omiten las pruebas unitarias y los cambios en App.Config al ejecutar pruebas unitarias](#UnitTestingAndAppConfigChanges)  
  
-   [Implementación de la base de datos en un destino inesperado al ejecutar pruebas unitarias](#DatabaseDeploymentInUnitTests)  
  
-   [Se agota el tiempo de espera al ejecutar pruebas unitarias en una base de datos](#TimeoutsDuringUnitTests)  
  
## <a name="UnitTestingAndAppConfigChanges"></a>Se omiten las pruebas unitarias y los cambios en App.Config al ejecutar pruebas unitarias  
Si modifica el archivo App.Config en el proyecto de prueba, debe recompilar el proyecto de prueba para que esos cambios surtan efecto. Entre estos cambios se incluyen los que realiza en App.Config mediante el cuadro de diálogo **Configuración de prueba de SQL Server**. Si no recompila el proyecto de prueba, los cambios no se aplicarán cuando ejecute las pruebas unitarias.  
  
## <a name="DatabaseDeploymentInUnitTests"></a>Implementación de la base de datos en un destino inesperado al ejecutar pruebas unitarias  
Si implementa una base de datos desde un proyecto de base de datos cuando ejecuta pruebas unitarias, la base de datos se implementa con la información de la cadena de conexión especificada en la configuración de las pruebas unitarias. La información de conexión especificada en las propiedades Debug del proyecto de base de datos no se usa para esta tarea, lo que le permite ejecutar pruebas unitarias de SQL Server en diferentes instancias de la misma base de datos.  
  
## <a name="TimeoutsDuringUnitTests"></a>Se agota el tiempo de espera al ejecutar pruebas unitarias en una base de datos  
Si las pruebas unitarias de la base de datos producen un error debido a que se ha agotado el tiempo de espera, aumente el período de tiempo de espera actualizando el archivo app.config en el proyecto de prueba. El tiempo de espera de conexión, definido en la cadena de conexión, especifica cuánto tiempo debe esperarse cuando la prueba unitaria se conecta al servidor. El tiempo de espera de comando, que debe definirse directamente en el archivo app.config, especifica cuánto tiempo debe esperarse cuando la prueba unitaria ejecuta el script de Transact\-SQL. Si tiene problemas con pruebas unitarias de ejecución prolongada, pruebe a aumentar el valor de tiempo de espera de comando en el elemento de contexto correspondiente. Por ejemplo, para especificar un tiempo de espera de comando de 120 segundos para el elemento **PrivilegedContext**, actualice app.config del modo siguiente:  
  
```  
<SqlUnitTesting_VS2010>  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\..\..\..\Visual Studio 2010\Projects\Database10\Database10\AdventureWorks.sqlproj"  
        Configuration="Debug" />  
    <DataGeneration ClearDatabase="true" />  
    <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="30" />  
    <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="120" />  
</SqlUnitTesting_VS2010>  
```  
  
## <a name="see-also"></a>Ver también  
[Cómo: Crear pruebas unitarias de SQL Server para funciones, desencadenadores y procedimientos almacenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[Cómo: Configurar una ejecución de prueba unitaria de SQL Server](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
