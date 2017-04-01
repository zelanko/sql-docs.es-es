---
title: "Replicaci&#243;n a Base de datos SQL | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación de Base de datos SQL"
  - "replicación, Base de datos SQL"
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Replicaci&#243;n a Base de datos SQL
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la replicación puede configurarse para [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 **Configuraciones admitidas:**  
  
-   La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta en local o una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en una máquina virtual de Azure en la nube. Para obtener más información, consulte [Información general sobre SQL Server en máquinas virtuales de Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] debe ser un suscriptor de inserción de un publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   No se pueden colocar la base de datos de distribución y los agentes de replicación en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
-   Se admite la replicación transaccional unidireccional y la de instantáneas. No se admite la replicación transaccional punto a punto ni la de mezcla.  
  
## Versiones  
 El publicador y el distribuidor deben estar al menos en una de las siguientes versiones:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] esperado en SP3  
  
 Al intentar configurar la replicación con una versión anterior puede producir error número MSSQL_REPL20084 (el proceso no pudo conectar al suscriptor.) y MSSQL_REPL40532 (no se puede abrir el servidor \< nombre> solicitada por el inicio de sesión. Error de inicio de sesión).  
  
 El suscriptor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] debe ser al menos V12 y puede estar en cualquier región.  
  
 Para usar todas las características de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] debe utilizar las versiones más recientes de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) y [las herramientas de datos de SQL Server](https://msdn.microsoft.com/library/mt204009.aspx).  
  
## Comentarios  
 La replicación puede configurarse mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o por medio de la ejecución de instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el publicador. No se puede configurar la replicación mediante el portal de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .  
  
 La replicación solo puede usar inicios de sesión de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 La tabla replicada debe tener una clave principal.  
  
 Debe tener una suscripción de Azure y una [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12 existente.  
  
 Una sola publicación en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede admitir ambos [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (locales y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina virtual de Azure) los suscriptores.  
  
 Administración de replicación, supervisión y solución de problemas debe realizarse desde las instalaciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Solo se admiten suscripciones de inserción a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .  
  
 Sólo `@subscriber_type = 0` se admite en **sp_addsubscription** base de datos SQL.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] no admite la replicación bidireccional, inmediata, puede actualizar o punto a punto.  
  
## Arquitectura de replicación  
 ![replication-to-sql-database](../../relational-databases/replication/media/replication-to-sql-database.png "replication-to-sql-database")  
  
## Escenarios  
  
#### Escenario típico de replicación  
  
1.  Crear una publicación de replicación transaccional en un local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
2.  En las instalaciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizar el **Asistente para nueva suscripción** o [!INCLUDE[tsql](../../includes/tsql-md.md)] las instrucciones para crear una inserción en la suscripción a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
3.  El conjunto de datos inicial es normalmente una instantánea que se crea con el Agente de instantáneas y se distribuye y aplica a través del Agente de distribución. También se puede suministrar el conjunto de datos inicial mediante una copia de seguridad u otro medio, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
#### Escenario de migración de datos  
  
1.  Usar la replicación transaccional para replicar datos desde una implementación local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la base de datos [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  Redirigir las aplicaciones cliente o nivel medio para actualizar el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] copia.  
  
3.  Detenga la actualización de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la tabla y quite la publicación.  
  
## Limitaciones  
 No se admiten las siguientes opciones para suscripciones de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] :  
  
-   Copiar asociaciones de grupos de archivos  
  
-   Copiar esquemas de particionamiento de tabla  
  
-   Copiar esquemas de particionamiento de índice  
  
-   Copiar estadísticas definidas por el usuario  
  
-   Copiar enlaces predeterminados  
  
-   Copiar enlaces de reglas  
  
-   Copiar índices de texto  
  
-   Copiar XML XSD  
  
-   Copiar índices XML  
  
-   Copiar permisos  
  
-   Copiar índices espaciales  
  
-   Copiar índices filtrados  
  
-   Copiar atributo de compresión de datos  
  
-   Copiar atributo de columna dispersa  
  
-   Convertir tipo de secuencia de archivos a tipos de datos MAX  
  
-   Convertir tipo hierarchyId a tipos de datos MAX  
  
-   Convertir tipo espacial a tipos de datos MAX  
  
-   Copiar propiedades extendidas  
  
-   Copiar permisos  
  
 Limitaciones que se han de determinar:  
  
-   Copiar intercalación  
  
-   Ejecución en una transacción serializada de SP  
  
## Ejemplos  
 Cree una publicación y una suscripción de inserción. Para obtener más información, vea:  
  
-   [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md) utilizando el [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] nombre del servidor lógico como el suscriptor (por ejemplo **N'azuresqldbdns.database.windows.net'**) y el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nombre como la base de datos de destino (por ejemplo **AdventureWorks**).  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Tipos de replicación](../../relational-databases/replication/types-of-replication.md)   
 [La supervisión de & #40; Replicación y nº 41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Inicializar una suscripción](../../relational-databases/replication/initialize-a-subscription.md)  
  
  