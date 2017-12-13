---
title: Usar reescrituras de cubos (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- writeback [Analysis Services], cubes
- cubes [Analysis Services], modifying
- modifying cubes
- UPDATE CUBE statement
- cubes [Analysis Services], writeback
ms.assetid: ae2385fc-7fa0-4f8e-98d7-dcb0a5f0eeea
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3306e20389ece189a8f40c449ea88aa640af4f0e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-data-modification---using-cube-writebacks"></a>Modificación de datos MDX - usar reescrituras de cubos
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Actualizar un cubo mediante la [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) instrucción. Esta instrucción permite actualizar una tupla con un valor específico. Para utilizar de forma eficaz la instrucción UPDATE CUBE a fin de actualizar, un cubo es preciso comprender la sintaxis de la instrucción, las condiciones de error que pueden generarse y el efecto de las actualizaciones en el cubo.  
  
## <a name="update-cube-statement-syntax"></a>Sintaxis de la instrucción UPDATE CUBE  
 La siguiente sintaxis describe la instrucción UPDATE CUBE:  
  
```  
UPDATE [CUBE] <Cube_Name> SET <tuple>.VALUE = <value> [,<tuple>.VALUE = <value>...]  
 [ USE_EQUAL_ALLOCATION | USE_EQUAL_INCREMENT |  
  USE_WEIGHTED_ALLOCATION [BY <weight value_expression>] |  
  USE_WEIGHTED_INCREMENT [BY <weight value_expression>] ]   
```  
  
 Si no se especifica un conjunto completo de coordenadas para la tupla, las que no se hayan especificado usarán el miembro predeterminado de la jerarquía. La tupla identificada debe hacer referencia a una celda agregada con la función [Sum](../../../mdx/sum-mdx.md) y no debe utilizar ningún miembro calculado como una de las coordenadas de la celda.  
  
 Podría decirse que la instrucción UPDATE CUBE es una subrutina que genera una serie de operaciones de reescritura individuales en celdas atómicas. Todas estas operaciones de reescritura individuales se acumulan después en la suma especificada.  
  
> [!NOTE]  
>  Si las celdas actualizadas no se superponen, se puede utilizar la propiedad de la cadena de conexión **Update Isolation Level** para mejorar el rendimiento de UPDATE CUBE. Para más información, vea <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
## <a name="example"></a>Ejemplo  
 Puede probar UPDATE CUBE con el grupo de medida Sales Targets del cubo Adventure Works. Este grupo de medida consta de las medidas agregadas mediante SUM, que es un requisito de UPDATE CUBE.  
  
1.  Habilite la reescritura para el grupo de medida Sales Targets de la base de datos Adventure Works. En Management Studio, haga clic con el botón derecho en un grupo de medida, elija **Opciones de reescritura**y, después, elija **Habilitar reescritura**.  
  
     Debe ver una nueva tabla de reescritura en la carpeta Writeback. El nombre de la tabla es WriteTable_Fact Sales Quota.  
  
2.  Abra una ventana de consulta MDX. Ejecute la instrucción SELECT siguiente para ver el valor original:  
  
    ```  
    SELECT [Measures].[Sales Amount Quota] on 0 ,  
    [Employee].[Employee Department].[Title].&[Sales Representative].children on 1  
    FROM [Adventure Works]  
  
    ```  
  
     Debe ver las cuotas de importe de venta para cada representante.  
  
3.  Ejecute la instrucción UPDATE CUBE para reescribir un nuevo valor. En este ejemplo, estamos estableciendo la cuota de importe de venta en 0. Como el nuevo valor es 0, no especifique ningún método de asignación.  
  
    ```  
    UPDATE CUBE [Adventure Works]   
    SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 0  
  
    ```  
  
4.  Vuelva a ejecutar la instrucción SELECT. Ahora debe ver cero para las cuotas.  
  
 El valor de reescritura está limitado a la sesión actual. Para conservar el valor entre distintos usuarios y sesiones, procese la tabla de reescritura. En Management Studio, haga clic con el botón derecho en WriteTable_Fact Sales Quota y elija **Procesar**.  
  
 Para especificar un método de asignación, el nuevo valor debe ser mayor que cero. En este ejemplo, el nuevo valor de Sales Amount Quota es dos millones y el método de asignación distribuye la cantidad entre todos los representantes de ventas.  
  
```  
UPDATE CUBE [Adventure Works]   
SET ([Measures].[Sales Amount Quota], [Employee].[Employee Department].[Department].&[Sales]) = 2000000   
USE_EQUAL_ALLOCATION  
```  
  
## <a name="error-conditions"></a>Condiciones de error  
 En la siguiente tabla se describe lo que puede hacer que una operación de reescritura genere un error y el resultado de tales errores.  
  
|Condición de error|Resultado|  
|---------------------|------------|  
|La actualización incluye miembros de la misma dimensión que no pueden coexistir.|La actualización generará un error. El espacio del cubo no contendrá la celda a la que se hace referencia.|  
|La actualización incluye una medida con origen en una medida de un tipo sin signo.|La actualización generará un error. Los incrementos exigen que la medida acepte valores negativos.|  
|La actualización incluye una medida que agrega elementos distintos de Sum.|Se genera un error.|  
|Se ha intentado realizar la actualización en un subcubo.|Se genera un error.|  
  
## <a name="affect-of-cube-changes"></a>Efecto de los cambios en el cubo  
 Los siguientes cambios no tienen ningún efecto sobre las reescrituras:  
  
-   Procesamiento de un cubo, los grupos de medida del cubo o las dimensiones del cubo.  
  
-   Agregar atributos a una dimensión.  
  
-   Agregar una nueva dimensión.  
  
-   Eliminar una dimensión que no incluye la reescritura.  
  
-   Agregar, modificar o eliminar una jerarquía.  
  
-   Agregar una nueva medida.  
  
 Los siguientes cambios no pueden llevarse a cabo sin eliminar los datos de la reescritura:  
  
-   Eliminar un atributo, o su jerarquía de atributos, si el atributo está incluido en la reescritura. Esto incluye eliminar explícitamente el atributo, o su jerarquía de atributos, o bien eliminar la dimensión primaria del atributo.  
  
-   Eliminar una medida incluida en la reescritura.  
  
-   Agregar un atributo sin un nivel **(Todos)** a una dimensión incluida en la reescritura.  
  
-   Cambiar la granularidad de dimensión de una dimensión incluida en la reescritura.  
  
## <a name="see-also"></a>Vea también  
 [Modificar datos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)  
  
  
