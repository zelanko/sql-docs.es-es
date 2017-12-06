---
title: "Convertir código de R para usarlo en R Services | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 06/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e861a139af2c4aad159920a6659a0598091439b8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="converting-r-code-for-use-in-r-services"></a>Convertir código de R para usarlo en R Services

Cuando mueve el código de R de R Studio o con otro entorno a SQL Server, a menudo el código funciona correctamente sin modificaciones adicionales cuando se agrega a la  *@script*  parámetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esto es especialmente cierto si ha desarrollado su solución mediante la **RevoScaleR** funciones, de forma que sea relativamente fácil cambiar contextos de ejecución.

En cambio, normalmente deberá modificar el código de R para ejecutarlo en SQL Server, tanto para aprovechar una mayor integración con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como para evitar una transferencia de datos costosa.

Para ver ejemplos de cómo se puede ejecutar el código de R en SQL Server, consulte estos tutoriales:

+ [Análisis de bases de datos para que el programador de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) se muestra cómo hacer que el código de R más modular incluyéndolo en procedimientos almacenados

+ [Soluciones de ciencia de datos-to-End](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) incluye una comparación de ingeniería de características en R y T-SQL

## <a name="how-the-data-science-process-changes-in-sql-server"></a>¿Cómo se cambia el proceso de ciencia de datos en SQL Server

Cuando se trabaja en un entorno de desarrollo de R dedicado como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] o RStudio, el flujo de trabajo típico consiste en extraer los datos en el equipo, analizar los datos de forma iterativa y, a continuación, escribir o mostrar los resultados. Sin embargo, cuando se migra código independiente para SQL Server, gran parte de este proceso puede simplificado o delegar a otras herramientas de SQL Server. Además, al hacerlo puede mejorar el rendimiento en muchos casos.

| Código externo | R en SQL Server |
|-------|-------|
| Introducir datos| Definir datos de entrada como una consulta SQL. Evitar el movimiento de datos. |
| Resumir y visualizar datos| Los gráficos pueden exportarse como imágenes o envía a una estación de trabajo remota.|
|Ingeniería de características| Usar R en bases de datos si no desea modificar el código, pero vistazo a optimizar las consultas. Investigue si podrían ser más eficaces para llamar a funciones de T-SQL o UDF personalizadas.|
|Parte de limpieza de datos del proceso de análisis| Realizar ingeniería de característica, extracción de características y la limpieza de datos de antemano como parte de los flujos de trabajo de datos.|
|Generar predicciones en un archivo| Predicciones de salida a una tabla para evitar el movimiento de datos. Encapsulado predecir funciones en los procedimientos almacenados para el acceso directo en las aplicaciones.|

## <a name="best-practices"></a>Procedimientos recomendados

+ Tome nota de las dependencias, como los paquetes necesarios, de antemano. En un entorno de prueba y desarrollo, podría ser conveniente instalar paquetes como parte del código, pero esto es una práctica incorrecta en un entorno de producción. Notifique al administrador para que los paquetes se puedan instalar y probar antes de implementar el código.

+ Haga una lista de comprobación de posibles problemas de tipos de datos. Documentar el esquema de los resultados esperados en cada sección del código.

+ Identifique los orígenes de datos principales, como datos de entrenamiento del modelo o datos de entrada para las predicciones, frente a orígenes secundarios como factores, variables adicionales de agrupación, etc. Asigne el conjunto de datos más grande al parámetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Cambie las instrucciones de los datos de entrada para trabajar directamente en la base de datos. En lugar de mover datos a un archivo CSV local o realizar las llamadas ODBC de repetidas, puede obtener un mejor rendimiento mediante el uso de consultas o vistas que se pueden ejecutar directamente en la base de datos SQL evita el movimiento de datos.

+ Use los planes de consultas de SQL Server para identificar las tareas que pueden realizarse en paralelo. Si la consulta de entrada se puede ejecutar en paralelo, establezca `@parallel=1` como parte de los argumentos a [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Por lo general, el procesamiento en paralelo con este indicador es posible siempre que SQL Server pueda trabajar con tablas con particiones o distribuir una consulta entre varios procesos y agregar los resultados al final.

  Normalmente, el procesamiento en paralelo con este indicador no es posible si entrena modelos mediante algoritmos que requieren que se lean todos los datos o si necesita crear agregados.

+ Siempre que sea posible, reemplace las funciones de R convencionales por funciones de **ScaleR** que admitan la ejecución distribuida. Para obtener más información, consulte [comparación de Base de R y funciones de R de escala](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Revise el código de R para determinar si hay pasos que se pueden realizar independientemente o de una manera más eficiente, mediante una llamada de procedimiento almacenado independiente. Por ejemplo, puede decidir realizar la ingeniería de características o la extracción de características por separado y agregar los valores en una columna nueva. 

  Utilizar T-SQL en lugar del código de R para basada en conjunto. Para obtener un ejemplo de una solución en R que se compara las UDF y R para las tareas de ingeniería de característica, vea [tutorial de ciencia de datos-to-End](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Usar el paquete de R **sqlrutils** para convertir el código en una sola función con claramente definidas entradas y salidas, que se pueden asignar fácilmente a los parámetros de procedimiento almacenado. Para obtener más información y ejemplos, vea [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).


## <a name="restrictions"></a>Restricciones

 Tenga en cuenta las siguientes restricciones al convertir el código de R:

### <a name="data-types"></a>Tipos de datos

-   Se admiten todos los tipos de datos de R. En cambio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite mayor variedad de tipos de datos que R, por lo que algunas conversiones de tipos de datos implícitas se realizan al enviar datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a R y viceversa. También deberá explícitamente cast o convert algunos datos.

- Se admiten valores NULL. R usa el `na` construcción de datos para representar un valor que falta, que es similar a un valor null.

Para obtener más información, consulte [tipos de datos y bibliotecas de R](../r/r-libraries-and-data-types.md).

### <a name="inputs-and-outputs"></a>Entradas y salidas

+ Puede definir un único conjunto de datos de entrada como parte de los parámetros de procedimiento almacenado. Esta consulta de entrada para el procedimiento almacenado puede ser una única instrucción SELECT válida. Se recomienda que use esta entrada del conjunto de datos más importantes y obtener conjuntos de datos más pequeños según sea necesario mediante llamadas a RODBC.

+ Llamadas a procedimientos almacenados precedidas de la ejecución no se puede usar como entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Todas las columnas del conjunto de datos de entrada deben asignarse a las variables del script de R. Las variables se asignan automáticamente por nombre. Por ejemplo, suponga que el script de R contiene una fórmula como esta:
    
    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
     Se produce un error si el conjunto de datos de entrada no contiene columnas con los nombres coincidentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour y DayOfWeek.

+ También puede proporcionar varios parámetros escalares como entrada. En cambio, las variables que se pasen como parámetros del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) deben asignarse a las variables en el código de R. De forma predeterminada, las variables se asignan por nombre.

+ Para incluir las variables de entrada escalares en la salida del código de R, anexe la palabra clave **OUTPUT** cuando defina la variable.

+ En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], el código de R se limita a generar un único conjunto de datos como un objeto data.frame. En cambio, también puede generar varias salidas escalares, incluidos los gráficos en formato binario y los modelos en formato varbinary.

+ Normalmente, puede generar el conjunto de datos devuelto por el script de R sin tener que especificar nombres de las columnas de salida, mediante la opción WITH RESULT SETS UNDEFINED. En cambio, las variables en el script de R que quiera enviar deben asignarse a los parámetros de salida SQL.

+ Si el script de R usa el argumento `@parallel=1`, debe definir el esquema de salida. El motivo es que SQL Server puede crear varios procesos para ejecutar la consulta en paralelo, con los resultados recopilados al final. Por lo tanto, se debe definir el esquema de salida para pueden crear los procesos en paralelo.

### <a name="dependencies"></a>Dependencias

 + Evite la instalación de paquetes desde el código de R. En SQL Server, deben instalarse paquetes de antemano.
 
  Asegúrese de instalar paquetes en la biblioteca de paquete predeterminado utilizada por servicios de aprendizaje de máquina. Para obtener más información, vea [administración de paquetes de R para SQL Server](../r/r-package-management-for-sql-server-r-services.md)
