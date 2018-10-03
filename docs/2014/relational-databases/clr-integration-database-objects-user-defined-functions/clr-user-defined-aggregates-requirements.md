---
title: Requisitos para agregados definidos por el usuario CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 44aee43742fdc451012a9516249c0558b3ce0d35
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129185"
---
# <a name="requirements-for-clr-user-defined-aggregates"></a>Requisitos para agregados definidos por el usuario de CLR
  Un tipo de un ensamblado CLR (Common Language Runtime) puede registrarse como una función de agregado definida por el usuario, siempre y cuando implemente el contrato de agregación necesario. Este contrato consta del atributo `SqlUserDefinedAggregate` y los métodos del contrato de agregación. El contrato de agregación incluye el mecanismo para guardar el estado intermedio de la agregación y el mecanismo para acumular nuevos valores, que consta de cuatro métodos: `Init`, `Accumulate`, `Merge` y `Terminate`. Cuando cumpla estos requisitos, podrá aprovechar al máximo de los agregados definidos por el usuario [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En las siguientes secciones de este tema se proporcionan detalles adicionales sobre la forma de crear y trabajar con agregados definidos por el usuario. Para obtener un ejemplo, vea [las funciones de agregado Invoking CLR User-Defined](clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Para obtener más información, consulte [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Métodos de agregación  
 La clase registrada como un agregado definido por el usuario debe admitir los métodos de instancia siguientes. Estos son los métodos que usa el procesador de consultas para calcular la agregación:  
  
|Método|Sintaxis|Descripción|  
|------------|------------|-----------------|  
|`Init`|Init() void público;|El procesador de consultas usa este método para inicializar el cálculo de la agregación. Este método se invoca una vez para cada grupo que el procesador de consultas agrega. El procesador de consultas puede optar por reutilizar la misma instancia de la clase de agregado para calcular los agregados de varios grupos. El método `Init` debe realizar cualquier operación limpieza necesaria con respecto a los usos anteriores de esta instancia y habilitarla para reiniciar un nuevo el cálculo de agregado.|  
|`Accumulate`|public void Accumulate (valor de tipo de entrada [, valor de tipo de entrada,...]);|Uno o varios parámetros que representan los parámetros de la función. *INPUT_TYPE* debe ser administrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos equivalente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado por el tipo de datos *input_sqltype* en el `CREATE AGGREGATE` instrucción. Para obtener más información, consulte [asignación de datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> En el caso de los tipos definidos por el usuario (UDT), el tipo de entrada es igual al tipo UDT. El procesador de consultas usa este método para acumular los valores de agregado. Debe invocarse una vez para cada valor en el grupo que se agrega. El procesador de consultas solamente realiza esta llamada después de llamar al método `Init` en la instancia dada de la clase de agregado. La implementación de este método debe actualizar el estado de la instancia para reflejar la acumulación del valor de argumento que se pasa.|  
|`Merge`|public void fusión mediante combinación (valor udagg_class);|Este método puede usarse para combinar otra instancia de esta clase de agregado con la instancia actual. El procesador de consultas usa este método para combinar varios cálculos parciales de una agregación.|  
|`Terminate`|return_type pública Terminate();|Este método completa el cálculo de agregado y devuelve el resultado de la agregación. El *return_type* debe ser administrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos que es el equivalente administrado de *return_sqltype* especificado en el `CREATE AGGREGATE` instrucción. El *return_type* también puede ser un tipo definido por el usuario.|  
  
### <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 Los parámetros con valores de tabla (TVP), tipos de tabla definidos por el usuario que se pasan a un procedimiento o función, proporcionan un modo eficaz de pasar varias filas de datos al servidor. Los TVP presentan una funcionalidad similar a las matrices de parámetros, pero proporcionan más flexibilidad y una mayor integración con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También proporcionan la posibilidad de obtener mayor rendimiento. Además, los TVP ayudan a reducir el número de ciclos de ida y vuelta al servidor. En lugar de enviar varias solicitudes al servidor, como con una lista de parámetros escalares, los datos pueden enviarse al servidor como un TVP. Un tipo de tabla definido por el usuario no puede pasarse como un parámetro con valores de tabla a un procedimiento almacenado administrado o a una función que se ejecuta en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como tampoco puede devolverse desde dicho procedimiento o función. Asimismo, los TVP no pueden usarse dentro del ámbito de una conexión de contexto. Sin embargo, un TVP puede usarse con SqlClient en procedimientos almacenados administrados o en funciones que se ejecutan en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si se usa en una conexión que no es de contexto. La conexión puede ser al mismo servidor que está ejecutando el procedimiento administrado o función. Para obtener más información acerca de Tvp, vea [usar parámetros &#40;motor de base de datos&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se ha actualizado la descripción del método `Accumulate`; ahora acepta más de un parámetro.|  
  
## <a name="see-also"></a>Vea también  
 [Tipos definidos por el usuario CLR](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Invocar funciones de agregado definidas por el usuario de CLR](clr-user-defined-aggregate-invoking-functions.md)  
  
  
