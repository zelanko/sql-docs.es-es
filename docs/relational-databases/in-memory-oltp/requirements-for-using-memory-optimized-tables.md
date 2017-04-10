---
title: "Requisitos para utilizar las tablas con optimizaci&#243;n para memoria | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: 65
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 65
---
# Requisitos para utilizar las tablas con optimizaci&#243;n para memoria
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Para usar OLTP en memoria en la base de datos de Azure, vea [Introducción a In-Memory (vista previa) en Base de datos SQL](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/).  
  
 Además de [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md), estos son los requisitos para usar OLTP en memoria:  
  
-   SQL Server 2016 SP1 (o posterior), cualquier edición. Para SQL Server 2014 y SQL Server 2016 RTM (pre-SP1) necesita la edición Evaluation, Developer o Enterprise.
    - Nota: OLTP en memoria necesita la versión de 64 bits de SQL Server.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita suficiente memoria para almacenar los datos en tablas con optimización para memoria e índices, así como memoria adicional para admitir la carga de trabajo en línea. Vea [Estimar los requisitos de memoria para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) para obtener más información.  

-   Cuando ejecute [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina virtual (VM), asegúrese de que haya suficiente memoria asignada a la VM para admitir la memoria necesaria para índices y tablas con optimización para memoria. Dependiendo de la aplicación host de VM, la opción de configuración para garantizar la asignación de memoria para la VM podría denominarse Reserva de memoria o, si se usa la memoria dinámica, RAM mínima. Asegúrese de que esta configuración sea suficiente para las necesidades de las bases de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   Espacio en disco libre equivalente al doble del tamaño de las tablas durables con optimización para memoria.  
  
-   El procesador debe admitir la instrucción **cmpxchg16b** para usar OLTP en memoria. Todos los procesadores de 64 bits modernos admiten la instrucción **cmpxchg16b**.  
  
     Si usa una máquina virtual y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra un error provocado por un procesador más antiguo, compruebe si la aplicación host de VM tiene una opción de configuración para permitir **cmpxchg16b**. Si no, puede usar Hyper-V, que admite **cmpxchg16b** sin necesidad de modificar ninguna opción de configuración.  
  
-   OLTP en memoria se instala como parte de **Servicios de Motor de base de datos**.  
  
     Para instalar la generación de informes ([Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (para administrar OLTP en memoria mediante el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ), [Descarga de SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).  
  
## <a name="important-notes-on-using-includehek2tokenhek2mdmd"></a>Información importante sobre el uso de [!INCLUDE[hek_2](../../includes/hek-2-md.md)]  
  
-   A partir de SQL Server 2016 no hay límite para el tamaño de las tablas con optimización para memoria más que la memoria disponible. En SQL Server 2014, el tamaño total en memoria de todas las tablas durables de una base de datos no debería superar los 250 GB para las bases de datos de SQL Server 2014. Para obtener más información, vea [Estimar los requisitos de memoria para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md).  
    - Nota: A partir de SQL Server 2016 SP1, las ediciones Standard y Express admiten OLTP en memoria, pero imponen cuotas con respecto a la cantidad de memoria que se puede usar para las tablas con optimización para memoria en una base de datos determinada. En la edición Standard es de 32 GB por base de datos; en la edición Express es de 352 MB por base de datos. 
  
-   Si crea una o más bases de datos con tablas con optimización para memoria, debe habilitar la inicialización instantánea de archivos (conceda el derecho de usuario SE_MANAGE_VOLUME_NAME a la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin la inicialización instantánea de archivos, los archivos de almacenamiento con optimización para memoria (datos y archivos delta) se inicializarán en el momento de la creación, lo cual puede tener un impacto negativo en el rendimiento de la carga de trabajo. Para obtener más información sobre la inicialización instantánea de archivos, vea [Inicialización de archivos de base de datos](http://msdn.microsoft.com/library/ms175935\(SQL.105\).aspx). Para obtener información sobre cómo habilitar la inicialización instantánea de archivos, vea [Cómo y por qué habilitar la inicialización instantánea de archivos](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx).  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  