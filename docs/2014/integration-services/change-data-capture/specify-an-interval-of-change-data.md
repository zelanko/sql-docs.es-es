---
title: Especificar un intervalo de datos modificados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],specifying interval
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8b839a64feb81a538f943d403733fee3772cce7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116392"
---
# <a name="specify-an-interval-of-change-data"></a>Especificar un intervalo de datos modificados
  En el flujo de control de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza una carga incremental de datos modificados, la primera tarea consiste en calcular los extremos del intervalo de cambios. Estos extremos son `datetime` valores y se almacenarán en variables de paquete para su uso posterior en el paquete.  
  
> [!NOTE]  
>  Para obtener una descripción del proceso general de diseño del flujo de control, vea [Captura de datos modificados &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="set-up-package-variables-for-the-endpoints"></a>Configurar variables de paquete para los extremos  
 Antes de configurar la tarea Ejecutar SQL para calcular los extremos, será necesario definir las variables de paquete que almacenarán dichos extremos.  
  
#### <a name="to-set-up-package-variables"></a>Para establecer las variables de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra un nuevo proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  En la ventana **Variables** , cree las variables siguientes:  
  
    1.  Crear una variable con el `datetime` tipo de datos para almacenar el punto inicial del intervalo.  
  
         En este ejemplo se utiliza el nombre de variable ExtractStartTime.  
  
    2.  Cree otra variable con el `datetime` tipo de datos para almacenar el punto final del intervalo.  
  
         En este ejemplo se utiliza el nombre de variable ExtractEndTime.  
  
 Si calcula los extremos en un paquete primario que ejecuta varios paquetes secundarios, puede utilizar las configuraciones de variables de paquete primario para pasar los valores de estas variables a cada paquete secundario. Para más información, vea [Tarea Ejecutar paquete](../control-flow/execute-package-task.md) y [Usar los valores de variables y parámetros en un paquete secundario](../use-the-values-of-variables-and-parameters-in-a-child-package.md).  
  
## <a name="calculate-a-starting-point-and-an-ending-point-for-change-data"></a>Calcular un punto inicial y un punto final para los datos modificados  
 Después de establecer las variables de paquete para los extremos del intervalo, puede calcular los valores reales para dichos extremos y asignarlos a las variables de paquete correspondientes. Dado que esos extremos son valores `datetime`, deberá usar funciones que puedan calcular o utilizar valores `datetime`. Tanto el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lenguaje de expresiones y Transact-SQL tienen funciones que operan con `datetime` valores:  
  
 Las funciones de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lenguaje de expresiones que funcionan con `datetime` valores  
 -   [DATEADD &#40;expresión de SSIS&#41;](../expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF &#40;expresión de SSIS&#41;](../expressions/datediff-ssis-expression.md)  
  
-   [DATEPART &#40;expresión de SSIS&#41;](../expressions/datepart-ssis-expression.md)  
  
-   [DÍA &#40;expresión de SSIS&#41;](../expressions/day-ssis-expression.md)  
  
-   [GETDATE &#40;expresión de SSIS&#41;](../expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE &#40;expresión de SSIS&#41;](../expressions/getutcdate-ssis-expression.md)  
  
-   [MES &#40;expresión de SSIS&#41;](../expressions/month-ssis-expression.md)  
  
-   [AÑO &#40;expresión de SSIS&#41;](../expressions/year-ssis-expression.md)  
  
 Las funciones de Transact-SQL que operan con `datetime` valores  
 [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql).  
  
 Antes de utilizar cualquiera de estas funciones de `datetime` para calcular los extremos, deberá determinar si el intervalo es fijo y se produce con regularidad. Por lo general, se prefiere aplicar regularmente en las tablas de destino los cambios que se han producido en las tablas de origen. Por ejemplo, puede aplicar esos cambios cada hora, diariamente o incluso semanalmente.  
  
 Una vez que decida si su intervalo de cambios es fijo o aleatorio, podrá calcular los extremos:  
  
-   **Calcular la fecha y hora de inicio**. Utilice la fecha y hora de finalización de la carga anterior como los valores actuales. Si utiliza un intervalo fijo para las cargas incrementales, puede calcular este valor utilizando la `datetime` funciones de Transact-SQL o de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lenguaje de expresiones. De lo contrario, es posible que tenga que conservar los extremos entre las ejecuciones y utilizar una tarea Ejecutar SQL o una tarea Script para cargar el extremo anterior.  
  
-   **Calcular la fecha y hora de finalización**. Si utiliza un intervalo fijo para las cargas incrementales, calcule la fecha y hora de finalización actuales como un desplazamiento de la fecha y hora de inicio. De nuevo, puede calcular este valor utilizando la `datetime` funciones de Transact-SQL o de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lenguaje de expresiones.  
  
 En el procedimiento siguiente, el intervalo de cambios utiliza un intervalo fijo y da por supuesto que el paquete de la carga incremental se ejecuta diariamente sin excepciones. De lo contrario, se perderían los datos modificados para los intervalos que faltan. El punto inicial del intervalo es la medianoche de anteayer, es decir, hace unas 24 a 48 horas. El punto final del intervalo es la medianoche de ayer, es decir, la noche anterior, hace unas 0 a 24 horas.  
  
#### <a name="to-calculate-the-starting-point-and-ending-point-for-the-capture-interval"></a>Para calcular el punto inicial y el punto final del intervalo de captura  
  
1.  En la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , agregue una tarea Ejecutar SQL al paquete.  
  
2.  Abra el **Editor de la tarea Ejecutar SQL**y en la página **General** del editor, seleccione las opciones siguientes:  
  
    1.  En **Conjunto de resultados**, seleccione **Fila única**.  
  
    2.  Configure una conexión válida con una base de datos de origen.  
  
    3.  En **SQLSourceType**, seleccione **Entrada directa**.  
  
    4.  En **SQLStatement**, escriba la siguiente instrucción SQL:  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  En la página **Conjunto de resultados** del **Editor de la tarea Ejecutar SQL**, asigne el resultado de ExtractStartTime a la variable de paquete ExtractStartTime y el resultado de ExtractEndTime a la variable de paquete ExtractEndTime.  
  
    > [!NOTE]  
    >  Al usar una expresión para establecer el valor de una variable de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , dicha expresión se evalúa cada vez que se accede al valor de la variable.  
  
## <a name="next-step"></a>Paso siguiente  
 Una vez calculados los puntos inicial y final de un intervalo de cambios, el paso siguiente consiste en determinar si están listos los datos modificados.  
  
 **Tema siguiente:** [Determinar si los datos modificados están preparados](determine-whether-the-change-data-is-ready.md)  
  
## <a name="see-also"></a>Vea también  
 [Usar Variables en paquetes](../use-variables-in-packages.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md)   
 [Tarea Ejecutar SQL](../control-flow/execute-sql-task.md)   
 [Tarea Script](../control-flow/script-task.md)  
  
  
