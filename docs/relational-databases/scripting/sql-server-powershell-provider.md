---
title: Proveedor de SQL Server PowerShell | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], provider
- PowerShell [SQL Server], SQL Server PowerShell Provider
- Providers [PowerShell]
- SMO [SQL Server], PowerShell
- PowerShell [SQL Server], SMO
- SQL Server Management Objects, PowerShell
ms.assetid: b97acc43-fcd2-4ae5-b218-e183bab916f9
caps.latest.revision: 61
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40b88611b6d25c2908a679b84f73ccad5b12cfbe
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-powershell-provider"></a>Proveedor de PowerShell de SQL Server
  El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell expone la jerarquía de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en rutas de acceso similares a las rutas de acceso al sistema de archivos. Puede usar las rutas de acceso con el fin de buscar un objeto y, luego, usar los métodos de los modelos de Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO) para realizar acciones en los objetos.  
  
## <a name="benefits-of-the-sql-server-powershell-provider"></a>Ventajas del proveedor de PowerShell de SQL Server  
 Las rutas de acceso que implementa el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilitan la revisión sencilla e interactiva de todos los objetos de una instancia de SQL Server. Puede navegar por las rutas de acceso mediante alias de Windows PowerShell similares a los comandos que se usan normalmente para navegar por las rutas de acceso al sistema de archivos.  
  
## <a name="the-sql-server-powershell-hierarchy"></a>Jerarquía de SQL Server PowerShell  
 Los productos cuyos datos o modelos de objetos se pueden representar en una jerarquía usan proveedores de Windows PowerShell para exponer las jerarquías. La jerarquía se expone mediante el uso de una unidad y una estructura parecidas a las que usa el sistema de archivos de Windows.  
  
 Cada proveedor de Windows PowerShell implementa una o varias unidades. Cada unidad es el nodo raíz de una jerarquía de objetos relacionados. El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa un SQLSERVER: unidad de disco. El proveedor también define un conjunto de carpetas principales para el SQLSERVER: unidad de disco. Cada carpeta y sus subcarpetas representan el conjunto de objetos a los que se puede tener acceso usando un modelo de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se centra en una subcarpeta de una ruta de acceso que se inicia con una de estas carpetas principales, se pueden usar los métodos del modelo de objetos asociado para realizar las acciones en el objeto representado por el nodo. En la tabla siguiente se muestran las carpetas de Windows PowerShell que implementa el proveedor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|Carpeta|Espacio de nombres del modelo de objetos de SQL Server|Objetos|  
|------------|---------------------------------------|-------------|  
|SQLSERVER:\SQL|<xref:Microsoft.SqlServer.Management.Smo><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Agent><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Broker><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.Mail>|Objetos de base de datos, como tablas, vistas y procedimientos almacenados.|  
|SQLSERVER:\SQLPolicy|<xref:Microsoft.SqlServer.Management.Dmf><br /><br /> <xref:Microsoft.SqlServer.Management.Facets>|Objetos de administración basada en directivas, como directivas y facetas.|  
|SQLSERVER:\SQLRegistration|<xref:Microsoft.SqlServer.Management.RegisteredServers><br /><br /> <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>|Objetos de servidor registrado, como los grupos de servidores y los servidores registrados.|  
|SQLSERVER:\Utility|<xref:Microsoft.SqlServer.Management.Utility>|Los objetos de utilidad, como las instancias administradas de [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|SQLSERVER:\DAC|<xref:Microsoft.SqlServer.Management.DAC>|Objetos de aplicación de capa de datos, como los paquetes DAC, y operaciones como la implementación de una DAC.|  
|SQLSERVER:\DataCollection|<xref:Microsoft.SqlServer.Management.Collector>|Objetos de recopilador de datos, como conjuntos de recopilación y almacenes de configuración.|  
|SQLSERVER:\IntegrationServices|<xref:Microsoft.SqlServer.Management.IntegrationServices>|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como proyectos, paquetes, y entornos.|  
|SQLSERVER: \ SQLAS|<xref:Microsoft.AnalysisServices>|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos como cubos, agregaciones, y dimensiones.|  
  
 Por ejemplo, puede usar la carpeta SQLSERVER:\SQL para iniciar rutas de acceso que puedan representar cualquier objeto admitido por el modelo de objetos SMO. La parte inicial de una ruta de acceso SQLSERVER:\SQL es SQLSERVER:\SQL\\*nombreDeEquipo*\\*nombreDeInstancia*. Los nodos que siguen al nombre de instancia alternan entre colecciones de objetos (como *Bases de datos* o *Vistas*) y nombres de objeto (como AdventureWorks2012). Los esquemas no se representan como clases de objeto. Cuando se especifica el nodo para un objeto de nivel superior en un esquema, como una tabla o una vista, se debe especificar el nombre de objeto en el formato *nombreDeEsquema.nombreDeObjeto*.  
  
 Esta es la ruta de acceso de la tabla Vendor en el esquema Purchasing de la base de datos AdventureWorks2012 en una instancia predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el equipo local:  
  
```  
SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 Para obtener más información acerca de la jerarquía del modelo de objetos SMO, vea [SMO Object Model Diagram](../../relational-databases/server-management-objects-smo/smo-object-model-diagram.md).  
  
 Los nodos de colección de una ruta de acceso se asocian con una clase de colecciones del modelo de objetos asociado. Los nodos de nombre de objeto se asocian con una clase de objetos del modelo de objetos asociado, como en la tabla siguiente.  
  
|Ruta de acceso|Clase SMO|  
|----------|---------------|  
|SQLSERVER:\SQL\MiPC\DEFAULT\Databases|<xref:Microsoft.SqlServer.Management.Smo.DatabaseCollection>|  
|SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012|<xref:Microsoft.SqlServer.Management.Smo.Database>|  
  
## <a name="sql-server-provider-tasks"></a>Tareas del proveedor de SQL Server  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo usar los cmdlets de Windows PowerShell para navegar por los nodos de una ruta de acceso, y en cada nodo obtener una lista de los objetos de ese nodo.|[Navegar por las rutas de acceso de SQL Server PowerShell](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md)|  
|Describe cómo usar los métodos y las propiedades de SMO para notificar y trabajar en el objeto representado por un nodo de una ruta de acceso. También describe cómo obtener una lista de los métodos y propiedades de SMO para ese nodo.|[Trabajar con rutas acceso de SQL Server PowerShell](../../relational-databases/scripting/work-with-sql-server-powershell-paths.md)|  
|Describe cómo convertir un nombre de recursos uniforme (URN) (URN) de SMO a una ruta de acceso del proveedor de SQL Server.|[Convertir URN en rutas de acceso del proveedor de SQL Server](../../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)|  
|Describe cómo abrir las conexiones de autenticación de SQL Server mediante el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De forma predeterminada, el proveedor usa conexiones con autenticación de Windows realizadas mediante las credenciales de la cuenta de Windows que ejecuta la sesión de Windows PowerShell.|[Administrar la autenticación en PowerShell del motor de base de datos](../../relational-databases/scripting/manage-authentication-in-database-engine-powershell.md)|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
