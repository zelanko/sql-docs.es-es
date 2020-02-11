---
title: Asignar parámetros de consulta a variables en una tarea ejecutar SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameterized SQL commands [Integration Services]
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- Execute SQL task [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 6a164349-dfcf-4995-80bc-d4e7aee52a83
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8863de6fc0418dbf502492ac20f7c5c846696aea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057796"
---
# <a name="map-query-parameters-to-variables-in-an-execute-sql-task"></a>asignar parámetros de consulta a variables en una tarea Ejecutar SQL

  En este tema se describe cómo utilizar una instrucción SQL con parámetros en la tarea Ejecutar SQL, y crear asignaciones entre las variables y los parámetros de la instrucción SQL.  
  
 Para más información sobre la tarea Ejecutar SQL, los marcadores de parámetros y los nombres de parámetros que se usan con diferentes tipos de conexión, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Para asignar un parámetro de consulta a una variable  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con el que desea trabajar.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Si el paquete no incluye en ese momento una tarea Ejecutar SQL, agregue una al flujo de control del paquete. Para obtener más información, vea [Agregar o eliminar una tarea o un contenedor en un flujo de control](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md) .  
  .  
  
5.  Haga doble clic en la tarea Ejecutar SQL.  
  
6.  Proporcione un comando SQL con parámetros en una de las siguientes maneras:  
  
    -   Use entrada directa y escriba el comando SQL en la propiedad SQLStatement.  
  
    -   Use entrada directa, haga clic en **Generar consulta**y luego cree un comando SQL mediante las herramientas gráficas proporcionadas por el Generador de consultas.  
  
    -   Use una conexión de archivo y luego haga referencia al archivo que contiene el comando SQL.  
  
    -   Use una variable y luego haga referencia a la variable que contiene el comando SQL.  
  
     Los marcadores de parámetros que utiliza en las instrucciones SQL con parámetros dependen del tipo de conexión que utiliza la tarea Ejecutar SQL.  
  
    |Tipo de conexión|Marcador de parámetro|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET y SQLMOBILE|@\<nombre del parámetro>|  
    |ODBC|?|  
    |EXCEL y OLE DB|?|  
  
     La tabla siguiente enumera ejemplos del comando SELECT por tipo de Administrador de conexiones. Los parámetros proporcionan los valores de filtro en las cláusulas WHERE. Los ejemplos utilizan el comando SELECT para devolver los productos de la tabla **Product** de [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] que tienen un valor de **ProductID** mayor y menor que los valores especificados por dos parámetros.  
  
    |Tipo de conexión|Sintaxis de SELECT|  
    |---------------------|-------------------|  
    |EXCEL, ODBC y OLE DB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
     Para obtener ejemplos de cómo usar parámetros con procedimientos almacenados, vea [Parameters and Return Codes in the Execute SQL Task](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
7.  Haga clic en **Asignación de parámetros**.  
  
8.  Para agregar una asignación de parámetros, haga clic en **Agregar**.  
  
9. Escriba un nombre en el cuadro **Nombre de parámetro** .  
  
     Los nombres de parámetros que utiliza dependen del tipo de conexión que utiliza la tarea Ejecutar SQL.  
  
    |Tipo de conexión|Nombre de parámetro|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2…|  
    |ADO.NET y SQLMOBILE|@\<nombre del parámetro>|  
    |ODBC|1, 2, 3…|  
    |EXCEL y OLE DB|0, 1, 2, 3…|  
  
10. En la lista **Nombre de variable** , seleccione una variable. Para más información, vea [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
11. En la lista **Dirección** , especifique si el parámetro es una entrada, una salida o un valor devuelto.  
  
12. En la lista **Tipo de datos** , seleccione el tipo de datos del parámetro.  
  
    > [!IMPORTANT]  
    >  El tipo de datos del parámetro debe ser compatible con el tipo de datos de la variable.  
  
13. Repita los pasos del 8 al 11 para cada parámetro en la instrucción SQL.  
  
    > [!IMPORTANT]  
    >  El orden de las asignaciones de parámetros debe ser el mismo que el orden en que aparecen los parámetros en la instrucción SQL.  
  
14. Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
 [Tarea Ejecutar SQL](control-flow/execute-sql-task.md)   
 [Parámetros y códigos de retorno en la tarea ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)   
 [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
  
