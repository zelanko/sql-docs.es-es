---
title: 'Cómo: especificar la dirección de parámetro con el controlador SQLSRV | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4004fa498c01e73c99204bb0d36ac4bded66a9b
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>Cómo especificar la dirección del parámetro con el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe cómo utilizar el controlador SQLSRV para especificar la dirección del parámetro cuando se llama a un procedimiento almacenado. La dirección del parámetro se especifica al construir una matriz de parámetros (paso 3) que se pasa a [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
### <a name="to-specify-parameter-direction"></a>Pasos para especificar la dirección de parámetro  
  
1.  Defina una consulta de Transact-SQL que llame a un procedimiento almacenado. Utilice signos de interrogación (?) en lugar de los parámetros que se transmiten al procedimiento almacenado. Por ejemplo, esta cadena llama a un procedimiento almacenado (UpdateVacationHours) que acepta dos parámetros:  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > Se recomienda llamar a procedimientos almacenados mediante sintaxis canónica. Para obtener más información sobre la sintaxis canónica, consulte [al llamar a un procedimiento almacenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
2.  Inicialice o actualice las variables PHP de los marcadores de posición en la consulta de Transact-SQL. Por ejemplo, en el siguiente código se inicializan los dos parámetros correspondientes al procedimiento almacenado UpdateVacationHours:  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > Las variables que se inicializan o actualizan a **Null**, **DateTime**o tipos de secuencia no se pueden usar como parámetros de salida.  
  
3.  Use las variables PHP del paso 2 para crear o actualizar una matriz de valores de parámetros que corresponden, en orden, para los marcadores de posición de parámetro en la cadena de Transact-SQL. Especifique la dirección de cada parámetro de la matriz. La dirección de cada parámetro se establece en uno de dos maneras: de forma predeterminada (para los parámetros de entrada) o mediante el uso de **SQLSRV_PARAM_\***  constantes (para los parámetros de salida y bidireccionales). Por ejemplo, en el siguiente código se especifica el parámetro *$employeeId* como parámetro de entrada, y el parámetro *$usedVacationHours* , como un parámetro bidireccional:  
  
    ```  
    $params = array(  
                     array($employeeId, SQLSRV_PARAM_IN),  
                     array($usedVacationHours, SQLSRV_PARAM_INOUT)  
                    );  
    ```  
  
    Para comprender la sintaxis con la que se especifica la dirección del parámetro en general, suponga que *$var1*, *$var2*y *$var3* corresponden a los parámetros de entrada, salida y bidireccionales, respectivamente. Puede especificar la dirección del parámetro de cualquiera de las maneras siguientes:  
  
    -   Especificar implícitamente el parámetro de entrada, especificar explícitamente el parámetro de salida y especificar explícitamente un parámetro bidireccional:  
  
        ```  
        array(   
               array($var1),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
    -   Especificar explícitamente el parámetro de entrada, especificar explícitamente el parámetro de salida y especificar explícitamente un parámetro bidireccional:  
  
        ```  
        array(   
               array($var1, SQLSRV_PARAM_IN),  
               array($var2, SQLSRV_PARAM_OUT),  
               array($var3, SQLSRV_PARAM_INOUT)  
               );  
        ```  
  
4.  Ejecutar la consulta con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o con [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) y [sqlsrv_execute](../../connect/php/sqlsrv-execute.md). Por ejemplo, en el código siguiente se utiliza la conexión *$conn* para ejecutar la consulta *$tsql* con los valores de parámetro especificados en *$params*:  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>Vea también  
[Recuperación de parámetros de salida con el controlador SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
