---
title: "Tutoriales de SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
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
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 31
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# Tutoriales de SQL Server R Services
Use estos tutoriales para obtener información sobre [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] y los escenarios de ciencia de datos que admite, incluidos:

+ Desarrollo de modelos en R y su implementación en SQL Server
+ Operacionalización de código de R mediante la implementación de una solución de R desarrollada por un científico de datos en un servidor o en otro entorno de producción.
+ Movimiento de datos entre R y SQL Server
+ Cómo usar contextos de cálculo locales y remotos
  

## <a name="a-namebkmkend-to-endadeveloping-an-end-to-end-advanced-analytics-solution"></a><a name="bkmk_end-to-end"></a>Desarrollo de una solución integral de análisis avanzado  

[Tutorial integral de ciencia de datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 

Experimente el proceso integral de ciencia de datos, desde la adquisición y el análisis de datos a la puntuación. Aprenderá a usar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a operacionalizar el modelo al guardarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
Importará el conjunto de datos de los taxis de Nueva York a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con PowerShell y explorará los datos con R. 

Luego generará un modelo predictivo e implementará el modelo de R a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la puntuación en modo de predicción única. 

  
Este tutorial está destinado a usuarios que estén familiarizados con R así como con herramientas de desarrollador como PowerShell y SQL Server Management Studio. Debe tener acceso a un entorno de desarrollo de R y estar familiarizado con los comandos de R. 
  
## <a name="a-namebkmkdatascienceadata-science-deep-dive"></a><a name="bkmk_dataScience"></a>Análisis detallado de ciencia de datos  

[Introducción a RevoScaleR y SQL Server](http://go.microsoft.com/fwlink/?LinkID=691640&clcid=0x809)  

Este tutorial es un buen comienzo para los científicos de datos o desarrolladores que ya están familiarizados con el lenguaje R y que quieren aprender sobre los paquetes mejorados de R y las funciones de Microsoft R por Revolution Analytics. 

Aprenderá a usar las funciones de los paquetes ScaleR para mover datos entre R y SQL, y cambiar los contextos de cálculo para adaptarse a una tarea en particular. Creará algunos modelos y trazados y los moverá entre el entorno de desarrollo y SQL Server.  
  
Este tutorial está destinado a usuarios que han estado usando R y quieren obtener más información sobre cómo RevoScaleR y SQL Server pueden mejorar la experiencia de R.

## <a name="in-database-advanced-analytics-for-the-sql-developer"></a>In-Database Advanced Analytics for SQL Developers (Análisis avanzado en base de datos para desarrolladores de SQL)  
  
[Análisis avanzado en base de datos para desarrolladores de SQL &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)

Cree e implemente una solución de análisis avanzado completa con [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este ejemplo se centra en cómo integrar el lenguaje R de código abierto con el motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aprenderá cómo ajustar el código de R en un procedimiento almacenado, guardar un modelo de R en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realizar llamadas con parámetros al modelo de R para la predicción. 
  
Este tutorial está destinado a desarrolladores de SQL, desarrolladores de aplicaciones o DBA de SQL que trabajarán con soluciones de R y quieren obtener información sobre cómo implementar modelos de R en SQL Server.  No es necesario ningún entorno de R; se proporciona todo el código de R y puede crear la solución completa usando solo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y herramientas conocidas de desarrollo de SQL y de inteligencia empresarial.   

## <a name="use-r-services-in-an-application"></a>Utilizar R Services en una aplicación

[Compilar una aplicación inteligente con SQL Server y R](https://www.microsoft.com/sql-server/developer-get-started/r)

En este tutorial aprenderá cómo se podría utilizar el aprendizaje automático en una empresa de alquiler de esquís para predecir alquileres futuros, lo que resulta muy útil para el plan de negocios y para el personal a la hora de satisfacer la futura demanda.


## <a name="using-r-code-in-t-sql"></a>Uso de código de R en T-SQL  

[Uso de código de R en Transact-SQL &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  

Esta es una serie de ejemplos independientes breves que muestran la sintaxis básica para el uso de R en [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Aprenderá a llamar al entorno de ejecución de R desde SQL, conocerá las diferencias clave en los tipos de datos entre R y SQL, encapsulará las funciones de R en código de SQL y ejecutará un procedimiento almacenado que guardará los resultados de R en una tabla de SQL.
  
Este tutorial está destinado a los usuarios que son nuevos en R Services y quieren conocer los conceptos básicos de cómo llamar a R mediante T-SQL. No se necesita ninguna experiencia en R, pero debe saber cómo utilizar SQL Server Management Studio o cualquier otra herramienta que pueda conectarse a una base de datos y ejecutar consultas de T-SQL sencillas.

  
## <a name="a-namebkmkprerequisitesaprerequisites"></a><a name="bkmk_Prerequisites"></a>Requisitos previos
  
Para ejecutar cualquiera de estos tutoriales, debe descargar e instalar **R Services (en bases de datos)** como se describe aquí: [Configurar SQL Server R Services (en bases de datos)](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

Después de ejecutar la configuración de SQL Server, no olvide estos pasos adicionales:
+ Habilitar R Services ejecutando *sp_configure*
+ Reiniciar el servidor
+ Asegurarse de que el servicio que llama al tiempo de ejecución de R tiene los permisos necesarios
+ Asegurarse de que el inicio de sesión SQL o la cuenta de usuario de Windows que usará para su código de R tiene los permisos necesarios para conectarse al servidor y a sus bases de datos

Si tiene algún problema, consulte este artículo donde aparecen algunos problemas comunes: [Preguntas más frecuentes sobre actualización e instalación (SQL Server R Services)](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).

Si todavía no tiene un entorno de desarrollo de R preferido, puede instalar una de estas herramientas para comenzar:

+ [Cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/)

Tenga en cuenta que las bibliotecas de R estándar son insuficientes para usar estos tutoriales; tanto el entorno de desarrollo de R como el equipo de SQL Server que ejecuta R deben tener los paquetes ScaleR de Microsoft. Para obtener más información sobre Microsoft R, consulte este artículo: [Productos de Microsoft R](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#compare-prods).

## <a name="additional-resources"></a>Recursos adicionales

Cuando haya terminado estos tutoriales, use los siguientes vínculos para ver ejemplos y escenarios más avanzados.
  
### <a name="end-to-end-solution-templates-for-key-machine-learning-tasks"></a>Plantillas de soluciones integrales para tareas clave de aprendizaje automático  

[Plantillas de aprendizaje automático con SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/).  

El equipo de aprendizaje automático de Microsoft proporciona un conjunto de plantillas personalizables que le ayudarán a impulsar una solución de aprendizaje automático para estas tareas clave de aprendizaje automático:  
* Detección de fraude  
* Predicción personalizada de abandono  
* Mantenimiento predictivo  
  
Se proporciona todo el código de T-SQL y R, así como instrucciones sobre cómo entrenar e implementar un modelo de puntuación mediante procedimientos almacenados de SQL Server. 

### <a name="sample-data-and-sample-scripts"></a>Datos y scripts de ejemplo  
Los ejemplos de productos para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] están disponibles en el Centro de descargas de Microsoft. Para obtener únicamente los ejemplos para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], seleccione el archivo zip y abra la carpeta **Análisis avanzados**.  Algunas instrucciones son de versiones anteriores, pero existe una demostración de detección de fraude de seguros basada en la ley de Benford y un sencillo tutorial de un modelo predictivo en un conjunto de datos muy pequeño (el conjunto de datos Iris) que puede ser útil para las demostraciones.
  
[Ejemplos de productos de SQL Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=49502)  
### <a name="learn-more-about-r"></a>Más información sobre R  
Para obtener más información sobre R en general, consulte uno de los numerosos recursos excelentes enumerados aquí: [Recursos del idioma R](http://revolutionanalytics.com/r-language-resources).  
  
Para obtener información adicional sobre los paquetes de R proporcionados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], consulte el  [sitio de Revolution Analytics](http://go.microsoft.com/fwlink/?LinkId=691541).  
  
Esta entrada de blog describe el proceso de uso de los paquetes y las funciones de R proporcionados por [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e incluye código de ejemplo: [Uso de R en SQL Server](http://blog.revolutionanalytics.com/2015/10/previewing-using-revolution-r-enterprise-inside-sql-server.html).  
  
## <a name="see-also"></a>Vea también  
[Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
[Características y tareas de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
