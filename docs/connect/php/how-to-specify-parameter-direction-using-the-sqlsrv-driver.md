---
title: Especificación de la dirección del parámetro con el controlador SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf8169b2efa1c3016e98b61b34e9710635ac0d76
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993371"
---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>Cómo especificar la dirección del parámetro con el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe cómo utilizar el controlador SQLSRV para especificar la dirección del parámetro cuando se llama a un procedimiento almacenado. La dirección del parámetro se especifica cuando se crea un parámetro de matriz (paso 3) que se transmite a [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
### <a name="to-specify-parameter-direction"></a>Pasos para especificar la dirección de parámetro  
  
1.  Defina una consulta de Transact-SQL que llame a un procedimiento almacenado. Utilice signos de interrogación (?) en lugar de los parámetros que se transmiten al procedimiento almacenado. Por ejemplo, esta cadena llama a un procedimiento almacenado (UpdateVacationHours) que acepta dos parámetros:  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > Se recomienda llamar a procedimientos almacenados mediante sintaxis canónica. Para obtener más información sobre la sintaxis canónica, vea [Llamar a un procedimiento almacenado](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md).  
  
2.  Inicialice o actualice las variables PHP de los marcadores de posición en la consulta de Transact-SQL. Por ejemplo, en el siguiente código se inicializan los dos parámetros correspondientes al procedimiento almacenado UpdateVacationHours:  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > Las variables que se inicializan o actualizan a **Null**, **DateTime**o tipos de secuencia no se pueden usar como parámetros de salida.  
  
3.  Use las variables PHP del paso 2 para crear o actualizar una matriz de valores de parámetro que se corresponden, en orden, con los marcadores de posición de la cadena de Transact-SQL. Especifique la dirección de cada parámetro de la matriz. La dirección de cada parámetro se establece de una de estas dos maneras: de forma predeterminada (para los parámetros de entrada) o mediante las constantes **SQLSRV_PARAM_\*** (para los parámetros de salida y bidireccionales). Por ejemplo, en el siguiente código se especifica el parámetro *$employeeId* como parámetro de entrada, y el parámetro *$usedVacationHours* , como un parámetro bidireccional:  
  
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
  
4.  Ejecute la consulta con [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) y [sqlsrv_execute](../../connect/php/sqlsrv-execute.md). Por ejemplo, en el código siguiente se utiliza la conexión *$conn* para ejecutar la consulta *$tsql* con los valores de parámetro especificados en *$params*:  
  
    ```  
    sqlsrv_query($conn, $tsql, $params);  
    ```  
  
## <a name="see-also"></a>Consulte también  
[Recuperación de parámetros de salida con el controlador SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)

[Recuperación de parámetros de entrada y salida con el controlador SQLSRV](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  
