---
title: Requisitos para los agregados definidos por el usuario de CLR Microsoft Docs
description: La integración de SQL Server CLR permite crear funciones de agregado personalizadas en código administrado. Deben implementar el contrato de agregación necesario.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dd27cf3751400d3902ddd4199daee8aeef78b80
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487972"
---
# <a name="clr-user-defined-aggregates---requirements"></a>Agregados definidos por el usuario de CLR: requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Un tipo de un ensamblado CLR (Common Language Runtime) puede registrarse como una función de agregado definida por el usuario, siempre y cuando implemente el contrato de agregación necesario. Este contrato consta del atributo **SqlUserDefinedAggregate** y los métodos del contrato de agregación. El contrato de agregación incluye el mecanismo para guardar el estado intermedio de la agregación y el mecanismo para acumular nuevos valores, que consta de cuatro métodos: **Init**, **Accumulate**, **Merge**y **Terminate**. Cuando haya cumplido estos requisitos, podrá aprovechar al máximo los [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]agregados definidos por el usuario en . En las siguientes secciones de este tema se proporcionan detalles adicionales sobre la forma de crear y trabajar con agregados definidos por el usuario. Para obtener un ejemplo, vea [Invocar funciones de agregado definidas por](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)el usuario de CLR .  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Para obtener más información, vea [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Métodos de agregación  
 La clase registrada como un agregado definido por el usuario debe admitir los métodos de instancia siguientes. Estos son los métodos que usa el procesador de consultas para calcular la agregación:  
  
|Método|Sintaxis|Descripción|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|El procesador de consultas usa este método para inicializar el cálculo de la agregación. Este método se invoca una vez para cada grupo que el procesador de consultas agrega. El procesador de consultas puede optar por reutilizar la misma instancia de la clase de agregado para calcular los agregados de varios grupos. El método **Init** debe realizar cualquier limpieza según sea necesario con respecto a los usos anteriores de esta instancia y permitirle reiniciar un nuevo cálculo agregado.|  
|**Acumular**|`public void Accumulate ( input-type value[, input-type value, ...]);`|Uno o varios parámetros que representan los parámetros de la función. *input_type* debe ser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos administrado equivalente al tipo de datos nativo especificado por *input_sqltype* en la instrucción **CREATE AGGREGATE.** Para obtener más información, vea Asignación de datos de [parámetros CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> En el caso de los tipos definidos por el usuario (UDT), el tipo de entrada es igual al tipo UDT. El procesador de consultas usa este método para acumular los valores de agregado. Debe invocarse una vez para cada valor en el grupo que se agrega. El procesador de consultas siempre llama a esto solo después de llamar al método **Init** en la instancia dada de la clase agregada. La implementación de este método debe actualizar el estado de la instancia para reflejar la acumulación del valor de argumento que se pasa.|  
|**Combinar**|`public void Merge( udagg_class value);`|Este método puede usarse para combinar otra instancia de esta clase de agregado con la instancia actual. El procesador de consultas usa este método para combinar varios cálculos parciales de una agregación.|  
|**Terminate**|`public return_type Terminate();`|Este método completa el cálculo de agregado y devuelve el resultado de la agregación. El *return_type* debe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ser un tipo de datos administrado que sea el equivalente administrado de *return_sqltype* especificado en la instrucción **CREATE AGGREGATE.** El *return_type* también puede ser un tipo definido por el usuario.|  
  
### <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 Los parámetros con valores de tabla (TVP), tipos de tabla definidos por el usuario que se pasan a un procedimiento o función, proporcionan un modo eficaz de pasar varias filas de datos al servidor. Los TVP presentan una funcionalidad similar a las matrices de parámetros, pero proporcionan más flexibilidad y una mayor integración con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También proporcionan la posibilidad de obtener mayor rendimiento. Además, los TVP ayudan a reducir el número de ciclos de ida y vuelta al servidor. En lugar de enviar varias solicitudes al servidor, como con una lista de parámetros escalares, los datos pueden enviarse al servidor como un TVP. Un tipo de tabla definido por el usuario no puede pasarse como un parámetro con valores de tabla a un procedimiento almacenado administrado o a una función que se ejecuta en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como tampoco puede devolverse desde dicho procedimiento o función. Asimismo, los TVP no pueden usarse dentro del ámbito de una conexión de contexto. Sin embargo, un TVP puede usarse con SqlClient en procedimientos almacenados administrados o en funciones que se ejecutan en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si se usa en una conexión que no es de contexto. La conexión puede ser al mismo servidor que está ejecutando el procedimiento administrado o función. Para obtener más información acerca de los TVP, vea [Usar parámetros con valores ](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)de tabla &#40;Motor de base de datosDatabase Engine&#41;.  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se ha actualizado la descripción del método **Accumulate;** ahora acepta más de un parámetro.|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Invocar funciones de agregado definidas por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  
