---
title: Usar Variables en paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 910d1699c8cd88f9f29d22b7f08a80337a25473d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926334"
---
# <a name="use-variables-in-packages"></a>Usar variables en paquetes
  Las variables son una adición útil y flexible para los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ; las variables pueden permitir la comunicación entre los objetos del paquete, y entre los paquetes primarios y secundarios. También se pueden utiliza variables en expresiones y scripts.  
  
## <a name="user-defined-variables-and-system-variables"></a>Variables del sistema y definidas por el usuario  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona variables del sistema y admite las variables definidas por el usuario. Al crear un paquete y agregar un contenedor o una tarea a un paquete, o crear un controlador de eventos, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye un conjunto de variables del sistema para el contenedor. Las variables del sistema contienen información útil sobre el paquete, el contenedor, la tarea o el controlador de eventos. Por ejemplo, en tiempo de ejecución, la variable del sistema **MachineName** contiene el nombre del equipo en el que se ejecuta el paquete y la variable **StartTime** , la hora a la que se empezó a ejecutar el paquete. Las variables del sistema son de solo lectura. Para más información, consulte [System Variables](system-variables.md).  
  
 Puede crear variables definidas por el usuario y utilizarlas en los paquetes. Las variables definidas por el usuario se pueden usar de muchas formas en [!INCLUDE[ssIS](../includes/ssis-md.md)]: en scripts, en las expresiones usadas por las restricciones de precedencia, el contenedor de bucles For, la transformación Columna derivada y la transformación División condicional, y en las expresiones de propiedad que actualizan los valores de las propiedades.  
  
 Por ejemplo, puede utilizar una variable definida por el usuario en la condición de evaluación del contenedor de bucles For. También puede asignar el valor de colección del enumerador de un contenedor de bucles Foreach a una variable y, si una tarea Ejecutar SQL utiliza una instrucción SQL con parámetros, puede asignar los parámetros de la instrucción a variables. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md).  
  
## <a name="variables-usage-scenarios"></a>Escenarios del uso de variables  
 Las variables se usan de muchas formas distintas en los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Es probable que observe que el desarrollo de un paquete no avanza mucho antes de que tenga que agregar al paquete una variable definida por el usuario para lograr la flexibilidad y facilidad de uso que requiere la solución. Según el escenario de que se trate, las variables del sistema también se usan a menudo.  
  
 **Expresiones de propiedad** Use variables para proporcionar valores en las expresiones de propiedad que definen las propiedades de los paquetes y los objetos de paquete. Por ejemplo, la expresión `SELECT * FROM @varTableName` contiene la variable `varTableName` , que actualiza la instrucción SQL ejecutada por la tarea Ejecutar SQL. La expresión `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`actualiza el paquete ejecutado por la tarea Ejecutar paquete, mediante la ejecución del paquete especificado en la variable `varPackageFirst` el primer día de cada mes y la ejecución del paquete especificado en la variable `varPackageOther` los demás días. Para más información, vea [Usar expresiones de propiedad en paquetes](expressions/use-property-expressions-in-packages.md).  
  
 **Expresiones de flujo de datos** Use variables para proporcionar los valores de las expresiones utilizadas por las transformaciones Columna derivada y División condicional para llenar columnas o dirigir filas de datos a distintas salidas de transformación. Por ejemplo, la expresión `@varSalutation + LastName`concatena el valor de la variable `VarSalutation` y el de la columna `LastName` . La expresión `Income < @HighIncome`dirige a un resultado las filas de datos cuyo valor de la columna `Income` es menor que el valor de la variable `HighIncome` . Para obtener más información, vea [Transformación Columna derivada](data-flow/transformations/derived-column-transformation.md), [Transformación División condicional](data-flow/transformations/conditional-split-transformation.md) y [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 **Expresiones de restricción de precedencia** Se deben proporcionar valores para su uso en restricciones de precedencia para determinar si se ejecuta el ejecutable restringido. Las expresiones se pueden usar con un resultado de la ejecución (satisfactoria, errónea, terminada), o en lugar de un resultado de la ejecución. Por ejemplo, si la expresión `@varMax > @varMin` resulta en el valor `true`, se ejecuta el ejecutable. Para obtener más información, vea [Agregar expresiones a las restricciones de precedencia](control-flow/precedence-constraints.md).  
  
 **Parámetros y códigos de retorno** Se deben proporcionar valores para los parámetros de entrada, o almacenar los valores de los parámetros de salida y los códigos de retorno. Para ello, se asignan las variables a los parámetros y códigos de retorno. Por ejemplo, si se establece la variable `varProductId` en 23 y se ejecuta la instrucción SQL `SELECT * from Production.Product WHERE ProductID = ?`, la consulta recupera el producto cuyo `ProductID` sea 23. Para obtener más información, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md) y [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
 **Expresiones del bucle For** Se deben proporcionar valores para su uso en las expresiones de inicialización, evaluación y asignación del bucle For. Por ejemplo, si la variable `varCount` es 2 y `varMaxCount` es 10, la expresión de inicialización es `@varCount`, la expresión de evaluación es  `@varCount < @varMaxCount`y la expresión de asignación es `@varCount =@varCount +1`, el bucle se repite 8 veces. Para más información, vea [Contenedor de bucles For](control-flow/for-loop-container.md).  
  
 **Configuraciones de variables de paquete primario** Los valores de los paquetes primarios se deben pasar a los paquetes secundarios. Los paquetes secundarios pueden tener acceso a las variables del paquete primario utilizando configuraciones de variables de paquete primario. Por ejemplo, si el paquete secundario debe usar los mismos datos que el paquete primario, el secundario puede definir una configuración de variables de paquete primario que especifique una variable establecida por la función GETDATE en el paquete primario. Para obtener más información, consulte [Execute Package Task](control-flow/execute-package-task.md) y [Package Configurations](../../2014/integration-services/package-configurations.md).  
  
 **Tarea Script y componente de script** Se debe proporcionar a la tarea Script o al componente de script una lista de variables de solo lectura o lectura/escritura, actualizar las variables de lectura/escritura del script y, después, usar los valores actualizados dentro o fuera del script. Por ejemplo, en el código `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`, la variable de script `numberOfCars` se actualiza con el valor de la variable `NumberOfCars`. Para más información, consulte [Using Variables in the Script Task](control-flow/script-task.md).  
  
## <a name="configurations-and-variables"></a>Configuraciones y variables  
 Para actualizar dinámicamente las variables, puede crear configuraciones para las variables, implementar las configuraciones con el paquete y después, actualizar los valores de las variables en el archivo de configuración al implementar los paquetes. El paquete utiliza los valores actualizados de las variables en tiempo de ejecución. Para obtener más información, vea [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md).  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>Para agregar, modificar y eliminar variables definidas por el usuario  
  
-   [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [Establecer las propiedades de una variable definida por el usuario](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
