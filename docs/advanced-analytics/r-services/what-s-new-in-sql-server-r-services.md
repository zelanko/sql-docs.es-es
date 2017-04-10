---
title: "Novedades de SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 35
---
# Novedades de SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] es una característica de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y SQL Server vNext que admite la ciencia de datos de escala empresarial.  R es el lenguaje de programación más popular para los análisis avanzados y ofrece un conjunto de paquetes increíblemente variado, así como una comunidad de desarrolladores dinámica y en constante expansión. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] le ayuda a adoptar el tremendamente popular lenguaje de código abierto R en su negocio. 
  
 > [!TIP] ¿Ya tiene SQL Server 2016 R Services?
 > Ahora puede instalar la versión más reciente de Microsoft R Server en las instancias de 2016 a fin de aprovechar las actualizaciones más frecuentes de los componentes de R. Para más información, consulte [Microsoft R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new).  

## <a name="whats-new-in-sql-server-vnext"></a>Novedades de SQL Server vNext
  
+ Presentación del paquete **MicrosoftML**

   MicrosoftML es un nuevo paquete de aprendizaje automático para R de los equipos de Microsoft R Server y Microsoft Data Science. MicrosoftML aporta una mayor velocidad, rendimiento y escala para controlar un gran corpus de datos de texto y datos de categorías de dimensiones elevadas en los modelos de R con unas pocas líneas de código. Además, los clientes de Microsoft R Server obtendrán acceso a cinco mecanismos de aprendizaje rápidos y muy precisos que se incluyen en Azure Machine Learning. 
   
   Para obtener más información, consulte [Usar el paquete MicrosoftML con SQL Server R Services](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md).
   
+ Administración de paquetes más sencilla para científicos de datos

  Ya no hace falta que recurra al administrador de bases de datos para instalar los paquetes de R que necesita en SQL Server. Las nuevas funciones de instalación y desinstalación de paquetes de **RevoScaleR** le permiten instalar y actualizar fácilmente los paquetes de R Services desde un equipo cliente. 
  
  Para el administrador de bases de datos, se incluyen nuevos roles en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] para administrar los permisos asociados con los paquetes, tanto en el nivel de instancia como en el nivel de base de datos. 
  
  Para obtener más información, consulte [Administración de paquetes de R para SQL Server R Services](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 
     
+ Nuevas funciones en **RevoScaleR** para leer y escribir objetos de modelo de R

  RevoScaleR ahora incluye nuevas funciones de serialización y un formato de almacenamiento de modelos más compacto para agilizar el proceso de cargar y leer un modelo. 
  
  Para obtener más información, consulte [Guardar y cargar objetos de R desde SQL Server mediante ODBC](../../advanced-analytics/r-services/save-and-load-r-objects-from-sql-server-using-odbc.md). 

+ Paquete **sqlrutils** para facilitar la integración de SQL

  Este paquete de R ayuda a generar la llamada de procedimiento almacenado de SQL para el código de R. Los procedimientos almacenados de SQL que se generen pueden usarse después en SQL Server R Services. Se proporcionan ejemplos para ayudarle a consolidar el código de R en una función que se puede parametrizar en un procedimiento almacenado de SQL.
  
  Para obtener más información, consulte [Generar un procedimiento almacenado de R para el código de R con el paquete sqlrutils](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md). 
  

+ Paquete **olapR** para una conectividad de SSAS sencilla

   Este nuevo paquete proporciona una nueva dimensión de conectividad para R y SQL Server Analysis Services que facilita el uso de datos OLAP para el análisis en R. Puede ejecutar consultas MDX existentes y obtener una trama de datos de R, o bien generar instrucciones MDX simples mediante la definición de ejes de cubo y segmentaciones de datos en código de R. 
   
   Para obtener más información, consulte [Uso de datos de cubos OLAP en R](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md).
   

  
## <a name="features-in-sql-server-2016-r-services-and-sql-server-vnext"></a>Características en SQL Server 2016 R Services y SQL Server vNext  
  
- Paquete **RevoScaleR** para un aprendizaje automático rápido y paralelizable con R.

-   Compatibilidad con los inicios de sesión de SQL y la autenticación integrada de Windows.  
    
-   Mejoras de rendimiento considerables, como la optimización de los procesos subsidiarios de SQL, que conectan R y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la compatibilidad con la paginación de datos para permitir el uso de datos de gran volumen, y el streaming para permitir un procesamiento rápido de miles de millones de filas. 
  
-   Uso de grupos de recursos de SQL Server para administrar la memoria que consumen los procesos de R. Para obtener más información, consulte [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  

### <a name="tools-and-setup"></a>Herramientas y configuración

-   Instalación fácil de todos los componentes. El Asistente para la instalación de SQL Server puede instalar **SQL Server R Services (en bases de datos)** o **Microsoft R Server (independiente)**.   Al ejecutar el Asistente para la instalación, elija R Services si va a configurar una instancia de SQL Server y elija R Server (independiente) si va a configurar una estación de trabajo de ciencia de datos.   Para obtener más información sobre las opciones de configuración, consulte [Configurar SQL Server R Services &#40;en bases de datos&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) o [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  

-   Si no necesita usar datos en SQL Server, considere la posibilidad de usar [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)], que se puede ejecutar en numerosas plataformas y proporciona escala empresarial y rendimiento al popular lenguaje de código abierto R. [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]. Para obtener más información, consulte [R Server &#40;independiente&#41;](../../advanced-analytics/r-services/r-server-standalone.md) o [Introducing R Server](https://msdn.microsoft.com/microsoft-r/rserver) (Presentación de R Server) en MSDN.

- Para actualizar la instancia de SQL Server 2016 y poder usar Microsoft R Server 9.0.1, use la [utilidad SqlBindR.exe](https://msdn.microsoft.com/library/mt791781.aspx).  

- [Cliente de Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-install) es un entorno de R gratuito que incluye todas las herramientas y las bibliotecas que se necesitan para crear soluciones de R que se ejecuten en R Services o R Server.  

-   Herramientas de R para Visual Studio es un complemento gratuito para Visual Studio con una excelente compatibilidad con R, que incluye ventanas de variables e interactivas estándar de R, IntelliSense para funciones de R, depuración y Markdown en R, así como exportación a Word y HTML.  Para obtener más información, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).  

## <a name="learn-more"></a>Más información
  
-  Hay recursos disponibles tanto para los científicos de datos que quieren obtener información sobre la integración de SQL Server como para los desarrolladores de SQL que quieren crear soluciones de R con T-SQL y el entorno familiar de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 
   + [Tutoriales de SQL Server R Services](https://msdn.microsoft.com/library/mt591993.aspx)
   + [Libro electrónico gratuito: Data Science with SQL Server 2016](https://mva.microsoft.com/ebooks/) (Ciencia de datos con SQL Server 2016)
 
+ Si realmente necesita soluciones predefinidas, las [plantillas de aprendizaje automático](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) del equipo de Microsoft Data Science muestran soluciones prácticas para tareas de análisis comunes, incluidos el mantenimiento predictivo y la prevención del abandono.
 

  
## <a name="see-also"></a>Vea también  
[Novedades de SQL Server vNext](../../sql-server/what-s-new-in-sql-server-vnext.md)
  