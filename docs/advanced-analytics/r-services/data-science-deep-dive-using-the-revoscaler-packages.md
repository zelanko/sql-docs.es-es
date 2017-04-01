---
title: "An&#225;lisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR | Microsoft Docs"
ms.custom: ""
ms.date: "09/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# An&#225;lisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR
Este tutorial es una introducción a los paquetes mejorados de R proporcionados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Aprenderá a usar el marco de trabajo empresarial escalable para la ejecución de paquetes de R en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].   Al usar estas funciones escalables de R, un científico de datos puede crear soluciones personalizadas de R que se ejecuten en contextos locales o de servidor, para admitir el análisis de grandes volúmenes de datos de alto rendimiento.  
  
En este tutorial obtendrá información sobre cómo ver datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y su estación de trabajo de R, analizar y trazar datos, y crear e implementar modelos.  
    
## Información general 
 
Para ilustrar la flexibilidad y la potencia de procesamiento de los paquetes ScaleR, moverá datos e intercambiará contextos de cálculo frecuentemente en este tutorial.

+ Los datos se han obtenido inicialmente de archivos CSV o archivos XDF. Importará los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando las funciones del paquete RevoScaleR.    
+ El entrenamiento de modelos y la puntuación se realizarán en el contexto de cálculo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
    Creará nuevas tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando las funciones **rx**, para guardar los resultados de puntuación.    
+ Creará trazados tanto en el servidor como en el contexto de cálculo local.  
+ Para entrenar el modelo, usará datos que ya están guardados en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Todos los cálculos se realizarán en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
+ Extraerá un subconjunto de datos y lo guardará como un archivo XDF para volver a usarlo en el análisis en su estación de trabajo local.    
+ Los nuevos datos que se usan durante el proceso de puntuación se extraen de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una conexión ODBC. Todos los cálculos se realizan en la estación de trabajo local. 
+ Por último, realizará una simulación basada en una función de R personalizada, mediante el contexto de cálculo del servidor.

### Comenzar ahora  

Este tutorial tarda aproximadamente una hora en completarse, sin incluir la configuración.  

-   [Lección 1: Trabajar con datos de SQL Server con R](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
-   [Lección 2: Crear y ejecutar scripts de R](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
-   [Lección 3: Transformar datos mediante R](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
-   [Lección 4: Analizar datos en el contexto del proceso local](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
-   [Lección 5: Crear una simulación sencilla](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  

      
### Público de destino  
  
Este tutorial está destinado a científicos de datos o a usuarios que ya están familiarizados de alguna manera con R y con las tareas de ciencia de datos incluida la exploración, los análisis estadísticos y la optimización de modelos.  En cambio, se proporciona todo el código, de manera que pueda ejecutar el código fácilmente y seguir las indicaciones, suponiendo que tiene los entornos de cliente y servidor requeridos.  
  
También debe estar familiarizado con la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] y saber cómo obtener acceso a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] u otras herramientas de base de datos como Visual Studio.  
  
> [!TIP]  
> Guarde el área de trabajo de R entre lecciones para que pueda seguir fácilmente desde donde se ha quedado.  
  
### Requisitos previos  
  
-   **Servidor de bases de datos compatible con R**  
  
    Instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y habilitar SQL Server R Services (en bases de datos). Este proceso se describe en los [Libros en pantalla de SQL Server 2016](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx).  
  
-   **Permisos de base de datos**  
  
    Para ejecutar las consultas usadas para entrenar el modelo, debe tener privilegios **db_datareader** en la base de datos donde se almacenan los datos.  
  
  
-   **Estación de trabajo de ciencia de datos**  
  
    Debe instalar los paquetes RevoScaleR. La manera más fácil de hacerlo es instalar Microsoft R Server (independiente) o el cliente de Microsoft R. Para obtener más información, consulte [Configurar un cliente de ciencia de datos](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx).
      
    > [!NOTE] 
    > No se admiten otras versiones de Revolution R Enterprise o Revolution R Open. 
    > 
    > Una distribución de código abierto de R, como R 3.2.2, no funcionará en este tutorial porque solo la función ScaleR puede usar contextos de cálculo remotos. 
  
-   **Paquetes adicionales de R**  
  
    Para este tutorial, debe instalar los siguientes paquetes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2** y **e1071**. Se proporcionan instrucciones como parte del tutorial.  
  
    Todos los paquetes también deben estar instalados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se va a realizar el entrenamiento. Es importante que los paquetes se instalen en la biblioteca de paquetes de R usada por SQL Server. **No instale los paquetes en una biblioteca de usuario.** Si no tiene permiso para instalar paquetes en esta carpeta, pida al administrador de la base de datos que agregue los paquetes.   
  
Para obtener más información, consulte [Requisitos previos para los tutoriales de ciencia de datos &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md).  
  
## Estrategias de datos para soluciones de R distribuidas
    
En general, antes de empezar a escribir y ejecutar scripts de R en el entorno de desarrollo local, debería dedicar un minuto a planear el uso de los datos y determinar dónde ejecutar cada parte de la solución para obtener el rendimiento óptimo.  

En este tutorial, obtendrá experiencia con las funciones de alto rendimiento para analizar datos y crear modelos y trazados que se incluyen en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Haremos referencia a estas funciones en general como ScaleR o Microsoft R para distinguirlas de las funciones derivadas de otros paquetes de código abierto de R. Para obtener más información sobre cómo Microsoft R difiere de R de código abierto, consulte esta [Guía de introducción](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#microsoft-r-products). 

Una ventaja clave de usar las funciones ScaleR es que admiten el uso de *orígenes de datos* locales o de servidor, y de *contextos de cálculo* locales o remotos.  Por consiguiente, a medida que trabaje con este tutorial, considere las estrategias de datos que necesite adoptar para sus propias soluciones.
  
-   **¿Qué tipo de análisis quiere realizar?** ¿Es para su uso personal exclusivamente o va a compartir los modelos, resultados o gráficos con otros usuarios?
 
    En este tutorial obtendrá información sobre cómo ver los resultados de un lado a otro entre su entorno de desarrollo y el servidor para facilitar el uso compartido y el análisis. 
  
-   **¿Admite el paquete de R que necesita la ejecución remota?** Todas las funciones de los paquetes ScaleR proporcionados por [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se pueden ejecutar en contextos de cálculo remotos y, potencialmente, usar la ejecución en paralelo. Por el contrario, las funciones de los paquetes de terceros puede que necesiten recursos adicionales para la ejecución de subproceso único. 
    
    En este tutorial obtendrá información sobre cómo cambiar entre los contextos de cálculo locales y remotos para aprovecharse de los recursos de servidor cuando sea necesario. También aprenderá a ajustar funciones de R estándar en *rxExec* para admitir la ejecución remota de las funciones de R arbitrarias.
    
  
-   **¿Dónde están los datos y cuáles son sus características?**  Si los datos residen localmente, debe decidir si actualizará todos los datos nuevos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o entrenará localmente y guardará solo el modelo en la base de datos. Pero cuando implemente en producción, puede que necesite entrenar desde datos empresariales y usar procesos ETL para limpiar y cargar los datos.  
  
-   Preguntas similares se aplican a los datos de puntuación. ¿Va a crear la canalización de datos para la puntuación de los datos en la estación de trabajo o va a usar orígenes de datos empresariales? ¿Debe realizarse la preparación y la limpieza de los datos como parte de los procesos ETL o está realizando un experimento de una sola vez?  

    En este tutorial obtendrá información sobre cómo mover datos de manera eficaz y segura entre su entorno de R local y SQL Server. 
  
-   **¿Qué contexto de cálculo debe usar?** Puede que quiera entrenar su modelo localmente en datos muestreados y, después, empezar a usar los datos del servidor para las pruebas y la producción.

    En este tutorial obtendrá información sobre cómo mover datos entre SQL Server y R con R. También aprenderá a trabajar con datos que usan archivos XDF y a procesar datos en fragmentos mediante las funciones ScaleR.  
  
 
  
## Paso siguiente  
[Lesson 1: Work with SQL Server Data using R &#40;Data Science Deep Dive&#41; [Lección 1: Trabajar con datos de SQL Server con R&#40;Análisis detallado de ciencia de datos&#41;]](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
  
  
