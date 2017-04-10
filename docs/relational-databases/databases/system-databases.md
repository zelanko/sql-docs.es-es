---
title: "Bases de datos del sistema | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "bases de datos del sistema [SQL Server]"
  - "mostrar datos de bases de datos del sistema"
  - "modificar datos del sistema"
  - "ver datos de bases de datos del sistema"
ms.assetid: 30468a7c-4225-4d35-aa4a-ffa7da4f1282
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Bases de datos del sistema
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye las siguientes bases de datos del sistema.  
  
|Base de datos del sistema|Descripción|  
|---------------------|-----------------|  
|[Base de datos maestra](../../relational-databases/databases/master-database.md)|Registra toda la información del sistema para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Base de datos msdb](../../relational-databases/databases/msdb-database.md)|La utiliza el Agente SQL Server para programar alertas y trabajos.|  
|[Base de datos model](../../relational-databases/databases/model-database.md)|Se utiliza como plantilla para todas las bases de datos creadas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las modificaciones hechas a la base de datos **model** , como el tamaño de la base de datos, la intercalación, el modelo de recuperación y otras opciones de base de datos, se aplicarán a las bases de datos que se creen con posterioridad.|  
|[Base de datos Resource](../../relational-databases/databases/resource-database.md)|Base de datos de solo lectura que contiene objetos del sistema que se incluyen con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los objetos del sistema persisten físicamente en la base de datos **Resource** , pero aparecen lógicamente en el esquema **sys** de cada base de datos.|  
|[Base de datos tempdb](../../relational-databases/databases/tempdb-database.md)|Área de trabajo que contiene objetos temporales o conjuntos de resultados intermedios.|  
  
## Modificar datos del sistema  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite a los usuarios actualizar directamente la información de objetos del sistema, como tablas del sistema, procedimientos almacenados del sistema y vistas de catálogo. En vez de eso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un completo conjunto de herramientas administrativas con las que los usuarios pueden administrar totalmente el sistema, los usuarios y los objetos de una base de datos. Entre ellas, figuran:  
  
-   Utilidades de administración, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   API de SQL-SMO. Permite a los programadores incluir funcionalidad completa para administrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sus aplicaciones.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] . Pueden utilizar procedimientos almacenados del sistema e instrucciones DDL de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 Estas herramientas protegen a las aplicaciones de cambios en los objetos del sistema. Por ejemplo, en ocasiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene que cambiar las tablas del sistema de nuevas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que admitan las nuevas funciones agregadas. Las aplicaciones que utilizan instrucciones SELECT que hacen referencia directa a tablas del sistema suelen basarse en el formato anterior de estas tablas. Los sitios tal vez no se puedan actualizar a una nueva versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta que hayan reescrito las aplicaciones que realizan operaciones de selección de las tablas del sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene en cuenta los procedimientos almacenados del sistema, DDL y las interfaces publicadas de SQL-SMO, y trabaja para mantener la compatibilidad con versiones anteriores de estas interfaces.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite la definición de desencadenadores en las tablas del sistema, debido a que podrían alterar el funcionamiento del sistema.  
  
> [!NOTE]  
>  Las bases de datos del sistema no pueden residir en directorios de recursos compartidos UNC.  
  
## Ver datos de bases de datos del sistema  
 No debe utilizar en sus programas instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que consulten directamente las tablas del sistema, a menos que ese sea el único modo de obtener la información que requiere la aplicación. En su lugar, las aplicaciones deben obtener información de catálogo y del sistema mediante el uso de:  
  
-   Vistas de catálogo del sistema.  
  
-   SQL-SMO.  
  
-   Interfaz de Instrumental de administración de Windows (WMI).  
  
-   Funciones de catálogo, métodos, atributos o propiedades de la API de datos usada en la aplicación, como ADO, OLE DB u ODBC.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados del sistema y funciones integradas.  
  
## Tareas relacionadas  
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Ocultar objetos del sistema en el Explorador de objetos](../../ssms/object/hide-system-objects-in-object-explorer.md)  
  
## Contenido relacionado  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
 [Bases de datos](../../relational-databases/databases/databases.md)  
  
  