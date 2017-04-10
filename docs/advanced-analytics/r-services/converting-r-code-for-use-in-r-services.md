---
title: "Convertir c&#243;digo de R para su uso en los servicios de R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Convertir c&#243;digo de R para su uso en los servicios de R
Al mover código R de R Studio o en otro entorno a SQL Server, a menudo el código funcionará sin modificaciones adicionales cuando se agrega a la *@script* parámetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esto es especialmente cierto si ha desarrollado la solución con las funciones de utilizar otros equipos, lo que relativamente simple cambiar contextos de ejecución.    
    
Sin embargo, normalmente deberá modificar su código R para ejecutar en SQL Server, tanto para aprovechar la integración más estrecha con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y evitar costosa transferencia de datos.   
   
   
## Recursos  
  
Para ver ejemplos de cómo se puede ejecutar código R en SQL Server, consulte estos tutoriales:   
+ [Análisis de base de datos para el desarrollador SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)    
  Muestra cómo puede hacer que el código de R más modular ajustando en procedimientos almacenados  
+ [Solución de ciencia de datos de extremo a extremo](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)    
  Incluye una comparación de ingeniería de características en R y T-SQL

## Cambios en el proceso de ciencia de datos en SQL Server  
  
Cuando se trabaja [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)], RStudio, o de otro entorno, un flujo de trabajo típico es extraer los datos en el equipo, analizar los datos de forma iterativa y, a continuación, escribir o mostrar los resultados. Sin embargo, cuando se migra código independiente R a SQL Server, gran parte de este proceso puede simplificado o delegar a otras herramientas de SQL Server:

| Código externo | R en SQL Server |
|-------|-------|
| Introducir datos| Definir los datos de entrada como una consulta SQL en la base de datos | 
| Resumir y visualizar datos| Sin cambios; se pueden exportar como imágenes o envía a una estación de trabajo remota trazados|
|Ingeniería de características| Puede usar R en bases de datos, pero puede ser más eficaz llamar a funciones de T-SQL o UDF personalizadas|
|Limpieza de la parte del proceso de análisis de datos| Limpieza de datos puede delegarse a los procesos ETL y realizar de antemano|
|Predicciones de salida en un archivo| Generar predicciones a la tabla o encapsular `predict` en los procedimientos almacenados para el acceso directo por las aplicaciones|
  

  
## Procedimientos recomendados  
  
+ Tome nota de las dependencias, como los paquetes necesarios, de antemano. En un entorno de prueba y desarrollo, podría ser conveniente instalar paquetes como parte del código, pero esto es una práctica incorrecta en un entorno de producción. Notificar al administrador para que los paquetes se pueden instalar y probar antes de implementar su código.  
+ Hacer una lista de comprobación de datos posibles problemas de tipo. Documente los esquemas de los resultados esperados en cada sección del código.  
+ Identifique los orígenes de datos principal como datos de entrenamiento del modelo o datos de entrada para las predicciones frente a orígenes secundarios como factores variables adicionales de agrupación y así sucesivamente. Asigne el conjunto de datos más grande al parámetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
+ Cambie las instrucciones de la entrada de datos para trabajar directamente en la base de datos. En lugar de mover datos a un archivo CSV local o realizar repite llamadas ODBC, obtendrá un rendimiento mejor mediante el uso de consultas o vistas que se pueden ejecutar directamente en la base de datos SQL evita el movimiento de datos.  
+ Los planes de consultas de SQL Server usar para identificar las tareas que pueden realizarse en paralelo. Si se puede paralelizar la consulta de entrada, establezca `@parallel=1` como parte de sus argumentos de sp_execute_external_script. Procesamiento con este indicador en paralelo es normalmente posible siempre que SQL Server puede trabajar con tablas con particiones o distribuir una consulta entre varios procesos y agregar los resultados al final. 
   Procesamiento con este indicador en paralelo normalmente no es posible si modelos de aprendizaje mediante algoritmos que requieren todos los datos de lectura, o si necesita crear agregados. 
+ Siempre que sea posible, reemplace las funciones de R convencionales con **utilizar otros equipos** funciones que admiten la ejecución distribuida. Para obtener más información, consulte [de las funciones de comparación en escala R y R CRAN](Summary%20of%20rx%20Functions.md).
+ Revise el código R para determinar si hay pasos que se pueden realizar independientemente o realizar más eficientemente, mediante una llamada de procedimiento almacenado independiente. Por ejemplo, puede realizar la extracción de ingeniería o característica características por separado y agregue los valores en una nueva columna. Utilizar T-SQL en lugar de código R para basada en conjunto. Para obtener un ejemplo de una solución de R que compara el rendimiento de las UDF y R para tareas de ingeniería de características, vea este tutorial: [Tutorial de extremo a extremo de ciencia de datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md).  
  
    
## Restricciones    
 Tenga en cuenta las siguientes restricciones al convertir código R:    
   
**Tipos de datos**    
-   Se admiten todos los tipos de datos de R. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con una gran variedad de tipos de datos de R, por lo que algunas conversiones de tipos de datos implícitas se realizan al enviar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos r y viceversa. También podría necesitar cast o convierta explícitamente algunos datos.    
    
- Se admiten valores NULL. R usa la `na` datos construcción para representar los valores que faltan, que es similar a los valores NULL.    
    
- Para obtener más información, consulte [trabajar con tipos de datos R](../../advanced-analytics/r-services/working-with-r-data-types.md).    
 
 **Entradas y salidas**   
+ Puede definir un único conjunto de datos de entrada como parte de los parámetros de procedimiento almacenado. Esta consulta de entrada para el procedimiento almacenado puede ser una única instrucción SELECT válida. Se recomienda que use esta entrada del conjunto de datos mayores y obtener conjuntos de datos más pequeños si es necesario mediante llamadas a RODBC. 

+ Precedido por la ejecución de llamadas no se puede utilizar como entrada de sp_execute_external_script del procedimiento almacenado.    
    
+ Todas las columnas del conjunto de datos de entrada deben asignarse a las variables del script de R. Las variables se asignan automáticamente por nombre. Por ejemplo, supongamos que su script de R contiene una fórmula como esta:    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     Se produce un error si el conjunto de datos de entrada no contiene columnas con los nombres coincidentes, ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour y DayOfWeek.    

+ También puede proporcionar varios parámetros escalares como entrada. Sin embargo, las variables que se pasen como parámetros del procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) deben asignarse a variables en el código de R. De forma predeterminada, las variables se asignan por nombre.
+ Para incluir las variables escalares de entrada en la salida del código R, anexar la **salida** palabra clave cuando defina la variable.             
+ En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], el código de R se limita a generar un único conjunto de datos como un objeto data.frame. Sin embargo, también puede generar escalares varias salidas, incluidos los gráficos en formato binario y los modelos en formato varbinary.    
    
+ Normalmente, puede generar el conjunto de datos devuelto por el script de R sin tener que especificar nombres de las columnas de salida mediante la opción con RESULT SETS UNDEFINED. Sin embargo, las variables en el script de R que se desea enviar deben asignarse a los parámetros de salida SQL.
    
+ Si el script de R utiliza el argumento `@parallel=1`, debe definir el esquema de salida. El motivo es que varios procesos pueden crearse mediante SQL Server para ejecutar la consulta en paralelo, con los resultados recopilados al final. Por lo tanto, el esquema de salida debe definirse antes de pueden crear los procesos en paralelo.

 **Dependencias**
 + Evite la instalación de paquetes de código R. En SQL Server, deben instalarse los paquetes de antemano.  
  
  
  

