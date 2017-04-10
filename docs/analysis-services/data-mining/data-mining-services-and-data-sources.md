---
title: "Servicios de miner&#237;a de datos y or&#237;genes de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 19
---
# Servicios de miner&#237;a de datos y or&#237;genes de datos
  La minería de datos requiere una conexión a una instancia de SQL Server Analysis Services. Los datos de un cubo no son necesarios para la minería de datos y se recomienda el uso de orígenes relacionales; sin embargo, la minería de datos usa los componentes proporcionados por el motor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 En este tema se proporciona información que es necesario conocer al conectarse a una instancia de SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para crear, procesar, implementar o consultar modelos de minería de datos.  
  
## Servicios de minería de datos  
 El componente de servidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es la aplicación msmdsrv.exe, que por lo general se ejecuta como un servicio de Windows. Esta aplicación está formada por componentes de seguridad, un componente de escucha XML for Analysis (XMLA), un componente de procesador de consultas y otros componentes internos que realizan las siguientes funciones:  
  
-   Analizar instrucciones recibidas de clientes  
  
-   Administrar metadatos  
  
-   Controlar transacciones  
  
-   Procesar cálculos  
  
-   Almacenar datos de celdas y dimensiones  
  
-   Crear agregaciones  
  
-   Programar consultas  
  
-   Almacenar objetos en memoria caché  
  
-   Administrar recursos del servidor  
  
### Componente de escucha XMLA  
 El componente de escucha XMLA controla todas las comunicaciones XMLA entre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y sus clientes. Puede utilizarse el valor de configuración [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Puerto** del archivo msmdsrv.ini para especificar un puerto en el que escucha una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Un valor de 0 en este archivo indica que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] escucha en el puerto predeterminado. A menos que se especifique lo contrario, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza los siguientes puertos TCP predeterminados:  
  
|Puerto|Description|  
|----------|-----------------|  
|2383|Instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|2382|Redirector de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|Se asigna dinámicamente al iniciar el servidor.|Instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
 Para más información sobre cómo controlar los puertos usados por este servicio, vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## Conectarse a orígenes de datos  
 Siempre que se crea o se actualiza un modelo o estructura de minería de datos, se utilizan los datos que se definen en un origen de datos. El origen de datos no contiene los datos, que podrían ser libros de Excel, archivos de texto y bases de datos de SQL Server; únicamente define la información de conexión.  Una vista del origen de datos (DSV) actúa como nivel de abstracción sobre el origen, modificando o asignando los datos que se obtienen del origen.  
  
 Está fuera del ámbito de este tema describir los requisitos de conexión de cada uno de estos orígenes. Para obtener más información, vea la documentación del proveedor. Sin embargo, en general, al interactuar con los proveedores debe tener en cuenta los siguientes requisitos de Analysis Services:  
  
-   Dado que la minería de datos es un servicio que proporciona un servidor, a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se le debe conceder acceso al origen de datos.  Hay dos aspectos para el acceso: la ubicación y la identidad.  
  
     **La ubicación** significa que, si genera un modelo con los datos almacenados solo en el equipo y luego implementa el modelo en un servidor, el modelo no podría procesarse porque el origen de datos no podría encontrarse. Para resolver este problema, puede que tenga que transferir datos de la misma instancia de SQL Server en la que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se está ejecutando o mover los archivos a una ubicación compartida.  
  
     **La identidad** significa que los servicios de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deben poder abrir el archivo de datos o el origen de datos con las credenciales adecuadas. Por ejemplo, al generar el modelo, podría haber tenido permisos ilimitados para ver los datos, pero el usuario que procesa y actualiza los modelos del servidor podría haber limitado o impedido el acceso a los datos, lo que podría impedir el procesamiento o afectar al contenido de un modelo. Como mínimo, la cuenta utilizada para conectarse al origen de datos remoto debe tener permisos de lectura en los datos.  
  
-   Al mover un modelo, se aplican los mismos requisitos: debe configurar el acceso adecuado a la ubicación del origen de datos antiguo, copiar los orígenes de datos o configurar un nuevo origen de datos. Además, debe transferir los inicios de sesión y los roles, o configurar los permisos para permitir que los objetos de minería de datos se procesen y actualicen en la nueva ubicación.  
  
## Configurar permisos y propiedades del servidor  
 La minería de datos requiere permisos adicionales en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La mayoría de las propiedades de minería de datos se pueden configurar con el [Cuadro de diálogo Propiedades de Analysis Server &#40;Analysis Services&#41;](../Topic/Analysis%20Server%20Properties%20Dialog%20Box%20\(Analysis%20Services\).md).  
  
 Para más información sobre las propiedades que se pueden configurar, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 Las siguientes propiedades del servidor son de especial relevancia para la minería de datos:  
  
-   **AllowAdHocOpenRowsetQueries** Controla el acceso ad hoc a los proveedores OLE DB, que se cargan directamente en el espacio de memoria del servidor.  
  
    > [!IMPORTANT]  
    >  Para mejorar la seguridad, se recomienda establecer esta propiedad en **false**. El valor predeterminado es **false**. Sin embargo, aunque esta propiedad esté establecida en **false**, los usuarios pueden continuar creando consultas singleton y pueden utilizar OPENQUERY en orígenes de datos permitidos.  
  
-   **AllowedProvidersInOpenRowset** Especifica el proveedor, si el acceso ad hoc está habilitado. Se pueden especificar varios proveedores, escribiendo una lista separada por comas de identificadores de programa.  
  
-   **MaxConcurrentPredictionQueries** Controla la carga en el servidor provocada por las predicciones. El valor predeterminado 0 permite consultas ilimitadas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise y un máximo de cinco consultas simultáneas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard. Las consultas que superan el límite se serializan y pueden agotar el tiempo de espera.  
  
 El servidor proporciona propiedades adicionales que controlan qué algoritmos de minería de datos están disponibles, incluida cualquier restricción en los algoritmos, y los valores predeterminados para todos los servicios de minería de datos. Sin embargo, no hay ninguna configuración que permita controlar el acceso a los procedimientos almacenados de minería de datos específicamente. Para más información, consulte [Data Mining Properties](../../analysis-services/server-properties/data-mining-properties.md).  
  
 También puede establecer propiedades que permitan ajustar el servidor y controlar la seguridad para uso del cliente. Para más información, consulte [Feature Properties](../../analysis-services/server-properties/feature-properties.md).  
  
> [!NOTE]  
>  Para más información sobre la compatibilidad de los algoritmos de complemento en las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que admiten la predicción de secuencias, vea [Características compatibles con las ediciones de SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
## Acceso a objetos de minería de datos mediante programación  
 Puede utilizar los modelos de objetos siguientes para crear una conexión a una base de datos de Analysis Services y trabajar con objetos de minería de datos:  
  
 **ADO** Usa OLE DB para conectarse a un servidor de Analysis Services. Cuando se utiliza ADO, el cliente está limitado a consultas de conjunto de filas de esquema e instrucciones DMX.  
  
 **ADO.NET** Interactúa con los proveedores de SQL Server mejor que con otros proveedores. Utiliza adaptadores de datos para almacenar conjuntos de filas dinámicos. Utiliza el objeto de conjunto de datos, que es una memoria caché de los datos del servidor almacenados como tablas de datos que se pueden actualizar o guardar como XML.  
  
 **ADOMD.NET** Un proveedor de datos administrado que se ha optimiza para trabajar con minería de datos y OLAP. ADOMD.NET es más rápido y usa la memoria con más eficacia que ADO.NET. ADOMD.NET también permite recuperar los metadatos acerca de los objetos de servidor. Se recomienda para las aplicaciones cliente excepto cuando .NET no está disponible.  
  
 **ADOMD de servidor** Modelo de objetos para tener acceso directo a los objetos de Analysis Services en el servidor. Lo usan los procedimientos almacenados de Analysis Services pero no el cliente.  
  
 **AMO** Interfaz de administración para Analysis Services que reemplaza a Objetos de ayuda para la toma de decisiones (DSO). Operaciones tales como la iteración de objetos requieren permisos superiores cuando se usa AMO que cuando se usan otras interfaces. Eso se debe a que AMO tiene acceso directo a los metadatos, mientras que ADOMD.NET y otras interfaces tienen acceso solamente a los esquemas de la base de datos.  
  
### Exploración y consulta del acceso a los servidores  
 Puede realizar cualquier tipo de predicciones con una instancia de Analysis Services en el modo de minería de datos y OLAP, con las restricciones siguientes:  
  
-   Si utiliza ADOMD de servidor, puede utilizar DMX para tener acceso al servidor sin realizar una conexión. A continuación, puede copiar directamente los resultados en una tabla de datos. Sin embargo, no puede utilizar ADOMD de servidor con instancias remotas; solo puede consultar el servidor local.  
  
-   ADO.NET no admite parámetros con nombre para la minería de datos. Debe utilizar ADOMD.NET.  
  
-   ADOMD.NET permite pasar una tabla completa para su uso como parámetro; por consiguiente, se pueden utilizar los datos en el cliente o los que no estén disponibles para el servidor. También se pueden utilizar tablas con forma como entrada de predicción.  
  
### Usar procedimientos almacenados de minería de datos  
 Un uso común de los procedimientos almacenados es encapsular las consultas para reutilizarlas. El cliente puede utilizar CALL para ejecutar procedimientos almacenados, incluidos los procedimientos almacenados de sistema de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Si el procedimiento devuelve un conjunto de datos, el cliente recibirá un conjunto de datos o una tabla de datos con una tabla anidada que contenga las filas. Por ejemplo, si crea una consulta con el contenido del modelo, esta devuelve el modelo completo. Para evitar que se devuelvan demasiadas filas, puede escribir los procedimientos almacenados con el modelo de objetos ADOMD+.  
  
 Para escribir un procedimiento almacenado de servidor, debe hacer referencia al espacio de nombres Microsoft.AnalysisServices.AdomdServer. Para obtener más información sobre cómo crear y usar procedimientos almacenados, vea [User Defined Functions and Stored Procedures](../../analysis-services/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures.md).  
  
> [!NOTE]  
>  Los procedimientos almacenados no se pueden utilizar para cambiar la seguridad en los objetos de servidor de datos. Cuando se ejecuta un procedimiento almacenado, el contexto actual del usuario se utiliza para determinar el acceso a todos los objetos de servidor. Por consiguiente, los usuarios deben disponer de los permisos adecuados en cualquier objeto de base de datos al que tengan acceso.  
  
## Vea también  
 [Arquitectura física &#40;Analysis Services - Datos multidimensionales&#41;](../Topic/Physical%20Architecture%20\(Analysis%20Services%20-%20Multidimensional%20Data\).md)   
 [Arquitectura física &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Administración de las soluciones y los objetos de minería de datos](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  