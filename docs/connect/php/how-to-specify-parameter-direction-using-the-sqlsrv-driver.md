---
title: "Cómo: especificar la dirección de parámetro con el controlador SQLSRV | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedure support
ms.assetid: 1209eeca-df75-4283-96dc-714f39956b95
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 404054a7d2fea19c6e8d0739f4497054ca8d3f2b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-specify-parameter-direction-using-the-sqlsrv-driver"></a>Cómo especificar la dirección del parámetro con el controlador SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se describe cómo utilizar el controlador SQLSRV para especificar la dirección del parámetro cuando se llama a un procedimiento almacenado. Tenga en cuenta que la dirección del parámetro se especifica cuando se crea un parámetro de matriz (paso 3) que se pasa a [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
### <a name="to-specify-parameter-direction"></a>Pasos para especificar la dirección de parámetro  
  
1.  Defina una consulta de Transact-SQL que llame a un procedimiento almacenado. Utilice signos de interrogación (?) en lugar de los parámetros que se transmiten al procedimiento almacenado. Por ejemplo, esta cadena llama a un procedimiento almacenado (UpdateVacationHours) que acepta dos parámetros:  
  
    ```  
    $tsql = "{call UpdateVacationHours(?, ?)}";  
    ```  
  
    > [!NOTE]  
    > Se recomienda llamar a procedimientos almacenados mediante sintaxis canónica. Para obtener más información sobre la sintaxis canónica, consulte [Llamar a un procedimiento almacenado](http://go.microsoft.com/fwlink/?linkid=119517).  
  
2.  Inicialice o actualice las variables PHP de los marcadores de posición en la consulta de Transact-SQL. Por ejemplo, en el siguiente código se inicializan los dos parámetros correspondientes al procedimiento almacenado UpdateVacationHours:  
  
    ```  
    $employeeId = 101;  
    $usedVacationHours = 8;  
    ```  
  
    > [!NOTE]  
    > Las variables que se inicializan o actualizan a **Null**, **DateTime**o tipos de secuencia no se pueden usar como parámetros de salida.  
  
3.  Use las variables PHP del paso 2 para crear o actualizar una matriz de valores de parámetros que corresponden, en orden, para los marcadores de posición de parámetro en la cadena de Transact-SQL. Especifique la dirección de cada parámetro de la matriz. La dirección de cada parámetro se establece en uno de dos maneras: de forma predeterminada (para los parámetros de entrada) o mediante el uso de **SQLSRV_PARAM_\* ** constantes (para los parámetros de salida y bidireccionales). Por ejemplo, en el siguiente código se especifica el parámetro *$employeeId* como parámetro de entrada, y el parámetro *$usedVacationHours* , como un parámetro bidireccional:  
  
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
[Cómo recuperar parámetros de salida con el controlador SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md)  
[How to: Retrieve Input and Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-input-and-output-parameters-using-the-sqlsrv-driver.md)  
  

