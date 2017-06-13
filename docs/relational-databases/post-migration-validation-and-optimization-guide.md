---
title: "Guía de optimización y posteriores a la migración validación | Documentos de Microsoft"
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: 
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: d81eabfa1bdb5736bbf6f53ed34c2e1ac157e782
ms.contentlocale: es-es
ms.lasthandoff: 05/25/2017

---
# <a name="post-migration-validation-and-optimization-guide"></a>Guía de optimización y validación posterior a la migración
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]registrar el paso de migración es muy fundamental para reconciliar cualquier precisión de los datos y la integridad, así como ayudan a solucionar problemas de rendimiento con la carga de trabajo.

# <a name="common-performance-scenarios"></a>Escenarios comunes de rendimiento 
A continuación se muestran algunos de los escenarios comunes de rendimiento que se encontró después de migrar a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] plataforma y cómo resolverlos. Puede tratarse de escenarios que resultan specifdic a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migración (versiones anteriores a las versiones más recientes), así como la plataforma externa (por ejemplo, Oracle, DB2, MySQL y Sybase) a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migración.

## <a name="Parameter Sniffing"></a>Sensibilidad a examen de parámetros

**Se aplica a:** plataforma externa (por ejemplo, Oracle, DB2, MySQL y Sybase) a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migración.

> [!NOTE]
> Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migraciones, si este problema existía en el origen de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrar a una versión más reciente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como-será no se contempla en este escenario. 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]compila los planes de consulta en procedimientos almacenados mediante el uso de examen de los parámetros de entrada en la primera compilación, generar un plan con parámetros y reutilizable, optimizado para que una entrada de distribución de datos. Incluso si no almacena los procedimientos, la mayoría de instrucciones generar planes triviales se se pueden parametrizar. Después de un plan en primer lugar se almacena en caché, cualquier ejecución futuras se asigna a un plan en caché previamente.
Un posible problema que surge cuando esa primera compilación puede no ha usado los conjuntos de parámetros más comunes para la carga de trabajo habitual. Para los parámetros diferentes, el mismo plan de ejecución pasa a ser ineficaz.

### <a name="steps-to-resolve"></a>Pasos para resolver

1.    Use la `RECOMPILE` sugerencia. Cada vez que adaptarse a cada valor de parámetro, se calcula un plan.
2.    Vuelva a escribir el procedimiento almacenado para usar la opción `(OPTIMIZE FOR(<input parameter> = <value>))`. Decidir qué valor desea usar se adapte a la mayor parte de la carga de trabajo relevante, crear y mantener un plan que pasa a ser eficaz para el valor con parámetros.
3.    Vuelva a escribir el procedimiento almacenado mediante la variable local dentro del procedimiento. Ahora el optimizador utiliza el vector de densidad para las estimaciones son erróneas, lo que produce el mismo plan sin tener en cuenta el valor del parámetro.
4.    Vuelva a escribir el procedimiento almacenado para usar la opción `(OPTIMIZE FOR UNKNOWN)`. Mismo efecto que usar la técnica de variable local.
5.    Vuelva a escribir la consulta para utilizar la sugerencia `DISABLE_PARAMETER_SNIFFING`. Mismo efecto que usar la técnica de la variable local por deshabilitar completamente el examen de parámetros, a menos que `OPTION(RECOMPILE)`, `WITH RECOMPILE` o `OPTIMIZE FOR <value>` se utiliza.

> [!TIP] 
> Aproveche el [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] característica de análisis de Plan para identificar rápidamente si se trata de un problema. Más información disponible [aquí](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/).

## <a name="Missing indexes"></a>Índices que faltan

**Se aplica a:** plataforma externa (por ejemplo, Oracle, DB2, MySQL y Sybase) y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migración.

Los índices que faltan o incorrectos hace E/S adicional que conduce a memoria adicional y CPU que se malgasta. Este puede ser porque ha cambiado el perfil de carga de trabajo como el uso de predicados diferentes, invalidando existente el diseño de índices. Evidencia de una estrategia de indexación deficiente o cambios en el perfil de carga de trabajo incluyen:
-   Busque duplicado, redundante, usado con poca frecuencia y los índices no usados por completo.
-   Especial cuidado con los índices no usados con las actualizaciones.

### <a name="steps-to-resolve"></a>Pasos para resolver

1.    Aprovechar el plan de ejecución gráfico para las referencias de índice que faltan.
2.    Indización sugerencias generadas por [el Asistente para la optimización de motor de base de datos](../tools/dta/tutorial-database-engine-tuning-advisor.md).
3.    Aproveche el [DMV de índices que faltan](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) o a través del [panel de rendimiento de SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=29063).
4.    Aprovechar las secuencias de comandos existentes que pueden utilizar DMV existentes para proporcionar una visión general de los índices que faltan, duplicados, redundantes, poco usados y completamente sin usar, sino también si cualquier referencia de índice se sugiere una/codificado de forma rígida en los procedimientos existentes y las funciones de la base de datos. 

> [!TIP] 
> Ejemplos de estos scripts preexistentes [creación de índices](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation) y [información del índice](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information). 

## <a name="Inability to use predicates"></a>Predicados de no pueden usar para filtrar los datos

**Se aplica a:** plataforma externa (por ejemplo, Oracle, DB2, MySQL y Sybase) y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migración.

> [!NOTE]
> Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migraciones, si este problema existía en el origen de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrar a una versión más reciente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como-será no se contempla en este escenario.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Optimizador de consultas sólo puede tener en cuenta para obtener información que se conoce en tiempo de compilación. Si una carga de trabajo se basa en predicados que solo pueden conocerse en tiempo de ejecución, a continuación, se aumenta la posibilidad de una opción de plan deficiente. Para un plan de mejor calidad, predicados deben ser **SARGable**, o **S**buscar **Arg**umentos**capaz de**.

Algunos ejemplos de predicados de no SARGable:
-   Conversiones implícitas de datos, como VARCHAR a NVARCHAR o INT a VARCHAR. Busque las advertencias de CONVERT_IMPLICIT de tiempo de ejecución en los planes de ejecución real. Convertir de un tipo a otro, también puede provocar una pérdida de precisión.
-   Las expresiones complejas indeterminadas como `WHERE UnitPrice + 1 < 3.975`, pero no `WHERE UnitPrice < 320 * 200 * 32`.
-   Expresiones que utilizan funciones, como `WHERE ABS(ProductID) = 771` o`WHERE UPPER(LastName) = 'Smith'`
-   Cadenas con un carácter comodín inicial, tales como `WHERE LastName LIKE '%Smith'`, pero no `WHERE LastName LIKE 'Smith%'`.

### <a name="steps-to-resolve"></a>Pasos para resolver

1. Declare siempre las variables o parámetros como el destino deseado [tipo de datos](../t-sql/data-types/data-types-transact-sql.md). 
  -   Esto puede implicar la comparación de cualquier construcción del código definido por el usuario que se almacena en la base de datos (por ejemplo, procedimientos almacenados, vistas o funciones definidas por el usuario) con las tablas del sistema que contienen información de tipos de datos utilizados en las tablas subyacentes (como [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md)).
2. Si no se puede recorrer todo el código hasta el punto anterior, con la misma finalidad, cambie el tipo de datos en la tabla para que coincida con las declaraciones de variable o parámetro.
3. La utilidad de las siguientes construcciones de motivo:
  -   Funciones que se usan como predicados;
  -   Búsquedas con caracteres comodín;
  -   Expresiones complejas en función de los datos en columnas: evaluar la necesidad de crear columnas calculadas persistentes, que se pueden indizar;

> [!NOTE] 
> Todo lo anterior puede realizarse programmaticaly.

## <a name="Table Valued Functions"></a>Uso de las funciones con valores de tabla (frente a varias instrucciones en línea)

**Se aplica a:** plataforma externa (por ejemplo, Oracle, DB2, MySQL y Sybase) y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migración.

> [!NOTE]
> Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] migraciones, si este problema existía en el origen de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], migrar a una versión más reciente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como-será no se contempla en este escenario.

Las funciones con valores de tabla devuelven un tipo de datos de tabla que puede ser una alternativa a las vistas. Mientras que las vistas se limitan a una sola `SELECT` (instrucción), funciones definidas por el usuario pueden contener instrucciones adicionales que permiten una lógica más que es posible en las vistas.

> [!IMPORTANT] 
> Puesto que no se creó la tabla de salida de un MSTVF (función con valores de tabla de múltiples instrucciones) en tiempo de compilación, el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] optimizador de consultas se basa en la heurística y las estadísticas no reales, para determinar las estimaciones de fila. Aunque los índices se agregan a las tablas base, esto no va a ayudar. Para MSTVFs, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza una estimación fija de 1 para el número de filas que se espera que va a devolver un MSTVF (a partir de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] que corrigen estimación es 100 filas).

### <a name="steps-to-resolve"></a>Pasos para resolver
1.    Si la función TVF de múltiples instrucciones es la única instrucción solo, convertir en Inline TVF.

    ```tsql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```
    Para 

    ```tsql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.    Si es más complejo, considere el uso de los resultados intermedios que se almacenan en tablas optimizadas en memoria o tablas temporales.

##  <a name="Additional_Reading"></a> Lecturas adicionales  
 [Procedimiento recomendado con el Almacén de consultas](../relational-databases/performance/best-practice-with-the-query-store.md)  
[Tablas con optimización para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[Funciones definidas por el usuario](../relational-databases/user-defined-functions/user-defined-functions.md)  
[Las Variables de tabla y fila estimaciones - parte 1](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[Las Variables de tabla y fila estimaciones - parte 2](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[Almacenamiento en caché del Plan de ejecución y reutilización](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)

