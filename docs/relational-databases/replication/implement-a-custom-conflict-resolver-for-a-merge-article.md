---
title: "Implementar un solucionador de conflictos personalizado para un art&#237;culo de mezcla | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], solucionadores basados en procedimiento almacenado"
  - "artículos [replicación de SQL Server], resolución de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Implementar un solucionador de conflictos personalizado para un art&#237;culo de mezcla
  Este tema describe cómo implementar el Solucionador de conflictos personalizado para un artículo de mezcla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)] o un [Solucionador personalizado basado en COM](../../relational-databases/replication/merge/com-based-custom-resolvers.md).  
  
 **En este tema**  
  
-   **Para implementar un solucionador de conflictos personalizado para un artículo de mezcla con:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Solucionador basado en COM](#COM)  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede escribir su propio solucionador de conflictos personalizado como un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] en cada publicador. Durante la sincronización, se llama a este procedimiento almacenado cuando se encuentran conflictos en un artículo para el que se registró el solucionador y el Agente de mezcla pasa información sobre la fila del conflicto a los parámetros pertinentes del procedimiento. Los solucionadores de conflictos personalizados basados en el procedimiento almacenado siempre se crean en el publicador.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resoluciones de procedimiento almacenado sólo se invocan para solucionar conflictos debidos a cambios de fila. No se pueden utilizar para solucionar otros tipos de conflictos como errores de inserción debidos a infracciones de CLAVE PRINCIPAL o a infracciones de restricción de índice único.  
  
#### Para crear un solucionador de conflictos personalizado basado en un procedimiento almacenado  
  
1.  En el publicador, ya sea en la publicación o en la base de datos **msdb** , cree un nuevo procedimiento almacenado del sistema que implemente los parámetros necesarios siguientes:  
  
    |Parámetro|Tipo de datos|Descripción|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|**sysname**|Nombre del propietario de la tabla en la que se resuelve un conflicto. Éste es el propietario de la tabla de la base de datos de publicación.|  
    |**@tablename**|**sysname**|Nombre de la tabla en la que se resuelve un conflicto.|  
    |**@rowguid**|**uniqueidentifier**|Identificador único de la fila que tiene el conflicto.|  
    |**@subscriber**|**sysname**|Nombre del servidor desde donde se propaga un cambio conflictivo.|  
    |**@subscriber_db**|**sysname**|Nombre de la base de datos desde donde se propaga un cambio conflictivo.|  
    |**@log_conflict OUTPUT**|**int**|Si el proceso de mezcla debería registrar un conflicto para su posterior resolución:<br /><br /> **0** = no registre el conflicto.<br /><br /> **1** = el suscriptor es el perdedor del conflicto.<br /><br /> **2** = publicador es el perdedor del conflicto.|  
    |**@conflict_message OUTPUT**|**nvarchar(512)**|Mensaje que se va a proporcionar sobre la resolución si se registra el conflicto.|  
    |**@destowner**|**sysname**|El propietario de la tabla publicada en el suscriptor.|  
  
     Este procedimiento almacenado utiliza los valores que pasa el Agente de mezcla a estos parámetros para implementar su lógica de resolución de conflictos personalizada; debe devolver un conjunto de resultados de filas único que sea idéntico en estructura a la tabla base y contenga los valores de datos de la versión ganadora de la fila.  
  
2.  Conceda permisos EXECUTE para el procedimiento almacenado a todos los inicios de sesión utilizados por los suscriptores para conectarse al publicador.  
  
#### Para utilizar un solucionador de conflictos personalizado con un nuevo artículo de tabla  
  
1.  Ejecutar [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir un artículo, especificando un valor de **MicrosoftSQL** **Server Stored Procedure Resolver** para el **@article_resolver** parámetro y el nombre del procedimiento almacenado que implementa la lógica de resolución de conflictos para el **@resolver_info** parámetro. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para utilizar un solucionador de conflictos personalizado con un artículo de tabla existente  
  
1.  Ejecutar [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, un valor de **article_resolver** para **@property**, y un valor de **MicrosoftSQL** **Server almacenan ProcedureResolver** para **@value**.  
  
2.  Ejecutar [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, un valor de **resolver_info** para **@property**, y el nombre del procedimiento almacenado que implementa la lógica de resolución de conflictos para **@value**.  
  
##  <a name="COM"></a> Usar un solucionador personalizado basado en COM  
 El <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> espacio de nombres implementa una interfaz que permite escribir lógica de negocios compleja para administrar eventos y resolver los conflictos que se producen durante el proceso de sincronización de replicación de mezcla. Para más información, consulte [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md). También puede escribir su propia lógica de negocios personalizada basada en código nativo para solucionar conflictos. Esta lógica está generada como componente COM y se compila en las bibliotecas de vínculo dinámico (DLL), usando productos como [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Este solucionador de conflictos personalizado basado en COM debe implementar la **ICustomResolver** interfaz, que está diseñado específicamente para la resolución de conflictos.  
  
#### Para crear y registrar un solucionador de conflictos personalizado basado en COM  
  
1.  En un entorno de creación compatible con COM, agregue referencias a la biblioteca del solucionador de conflictos personalizado.  
  
2.  Para un proyecto de Visual C++, use la directiva #import para importar esta biblioteca en su proyecto.  
  
3.  Cree una clase que implemente la interfaz **ICustomResolver** .  
  
4.  Implemente determinados métodos y propiedades.  
  
5.  Genere el proyecto para crear el archivo de biblioteca del solucionador de conflictos personalizado.  
  
6.  Implemente la biblioteca en el directorio que contiene la aplicación ejecutable del Agente de mezcla (normalmente \Microsoft SQL Server\100\COM).  
  
    > [!NOTE]  
    >  Se debe implementar un solucionador de conflictos personalizado en el Suscriptor para una suscripción de extracción, en el Distribuidor para una suscripción de inserción, o en el servidor web usado con sincronización web.  
  
7.  Registre la biblioteca del solucionador de conflictos personalizado usando regsvr32.exe desde el directorio de implementación de la siguiente manera:  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) Para comprobar que la biblioteca no está registrada como una resolución de conflictos personalizado.  
  
9. Para registrar la biblioteca como Solucionador de conflictos personalizado, ejecute [sp_registercustomresolver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), en el distribuidor. Especifique el nombre descriptivo del objeto COM para **@article_resolver**, Id. (CLSID de la biblioteca) para **@resolver_clsid**, y un valor de **false** para **@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Cuando ya no necesite un solucionador de conflictos personalizado puede ser registro mediante [sp_unregistercustomresolver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md).  
  
10. (Opcional) En un clúster, repita los pasos 5-8 para registrar el solucionador personalizado en todos los nodos del clúster. Esto es necesario para asegurar que el solucionador personalizado pueda cargar correctamente la reconciliación tras una conmutación por error.  
  
#### Para utilizar un solucionador de conflictos personalizado con un nuevo artículo de tabla  
  
1.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y anote el nombre descriptivo del solucionador que desee.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definir un artículo. Especifique el nombre descriptivo de la resolución de artículos del paso 1 para **@article_resolver**. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para utilizar un solucionador de conflictos personalizado con un artículo de tabla existente  
  
1.  En el publicador, ejecute [sp_enumcustomresolvers & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) y anote el nombre descriptivo del solucionador que desee.  
  
2.  Ejecutar [sp_changemergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), especificando **@publication**, **@article**, un valor de **article_resolver** para **@property**, y el nombre descriptivo de la resolución de artículos del paso 1 para **@value**.  
  
#### Ver un solucionador personalizado de ejemplo  
  
1.  Hay un ejemplo disponible en los archivos de ejemplo de SQL Server 2000. Descargue el archivo **sql2000samples.cab** desde [Ejemplos actualizados para SQL Server 2000 Service Pack 3](http://www.microsoft.com/download/details.aspx?id=8560). Se descargan 8 archivos que ocupan 6,9 MB.  
  
2.  Extraiga los archivos del archivo comprimido .cab descargado.  
  
3.  Ejecute **setup.exe**.  
  
    > [!NOTE]  
    >  Al elegir las opciones de instalación, solo es necesario instalar los ejemplos de **Replicación** . (La ruta de instalación predeterminada es **C:\Program archivos (x86) \Microsoft SQL Server 2000 Samples\1033\\**)  
  
4.  Vaya a la carpeta de instalación. (La carpeta predeterminada es **C:\Program archivos (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  Ejecute el **unzip_sqlreplSP3.exe** programa.  
  
    > [!NOTE]  
    >  Se instalará el solucionador com de ejemplo (de forma predeterminada) en el **C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** carpeta.  
  
6.  En el **subspres** carpeta, buscar todas las apariciones de **#include SQLRES** en todos los archivos de código fuente y reemplácelas con **#import "replrec.dll" no_namespace, raw_interfaces_only**  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Solucionadores personalizados para COM](../../relational-databases/replication/merge/com-based-custom-resolvers.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  