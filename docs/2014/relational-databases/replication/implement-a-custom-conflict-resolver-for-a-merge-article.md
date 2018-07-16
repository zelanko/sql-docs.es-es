---
title: Implementar un solucionador de conflictos personalizado para un artículo de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d0a94b6e958626e429711bb643cecc7bb87592c1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292296"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>Implementar un solucionador de conflictos personalizado para un artículo de mezcla
  En este tema se describe cómo implementar el solucionador de conflictos personalizado para un artículo de mezcla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] o un [solucionador personalizado basado en COM](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
 **En este tema**  
  
-   **Para implementar un solucionador de conflictos personalizado para un artículo de mezcla con:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Solucionador basado en COM](#COM)  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede escribir su propio solucionador de conflictos personalizado como un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] en cada publicador. Durante la sincronización, se llama a este procedimiento almacenado cuando se encuentran conflictos en un artículo para el que se registró el solucionador y el Agente de mezcla pasa información sobre la fila del conflicto a los parámetros pertinentes del procedimiento. Los solucionadores de conflictos personalizados basados en el procedimiento almacenado siempre se crean en el publicador.  
  
> [!NOTE]  
>  Los solucionadores de procedimientos almacenados de[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo se invocan para solucionar conflictos debidos a cambios de filas. No se pueden utilizar para solucionar otros tipos de conflictos como errores de inserción debidos a infracciones de CLAVE PRINCIPAL o a infracciones de restricción de índice único.  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>Para crear un solucionador de conflictos personalizado basado en un procedimiento almacenado  
  
1.  En el publicador, ya sea en la publicación o en la base de datos **msdb** , cree un nuevo procedimiento almacenado del sistema que implemente los parámetros necesarios siguientes:  
  
    |Parámetro|Tipo de datos|Descripción|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|Nombre del propietario de la tabla en la que se resuelve un conflicto. Éste es el propietario de la tabla de la base de datos de publicación.|  
    |**@tablename**|`sysname`|Nombre de la tabla en la que se resuelve un conflicto.|  
    |**@rowguid**|`uniqueidentifier`|Identificador único de la fila que tiene el conflicto.|  
    |**@subscriber**|`sysname`|Nombre del servidor desde donde se propaga un cambio conflictivo.|  
    |**@subscriber_db**|`sysname`|Nombre de la base de datos desde donde se propaga un cambio conflictivo.|  
    |**@log_conflict OUTPUT**|`int`|Si el proceso de mezcla debería registrar un conflicto para su posterior resolución:<br /><br /> **0** = No registre el conflicto.<br /><br /> **1** = El suscriptor es el perdedor del conflicto.<br /><br /> **2** = El publicador es el perdedor del conflicto.|  
    |**@conflict_message OUTPUT**|`nvarchar(512)`|Mensaje que se va a proporcionar sobre la resolución si se registra el conflicto.|  
    |**@destowner**|`sysname`|El propietario de la tabla publicada en el suscriptor.|  
  
     Este procedimiento almacenado utiliza los valores que pasa el Agente de mezcla a estos parámetros para implementar su lógica de resolución de conflictos personalizada; debe devolver un conjunto de resultados de filas único que sea idéntico en estructura a la tabla base y contenga los valores de datos de la versión ganadora de la fila.  
  
2.  Conceda permisos EXECUTE para el procedimiento almacenado a todos los inicios de sesión utilizados por los suscriptores para conectarse al publicador.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Para utilizar un solucionador de conflictos personalizado con un nuevo artículo de tabla  
  
1.  Ejecute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir un artículo, especificando el valor **MicrosoftSQL** **Server Stored Procedure Resolver** para el parámetro **@article_resolver** y el nombre del procedimiento almacenado que implementa la lógica del solucionador de conflictos para el parámetro **@resolver_info** . Para más información, consulte [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Para utilizar un solucionador de conflictos personalizado con un artículo de tabla existente  
  
1.  Ejecute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, un valor de **article_resolver** para **@property** y un valor de **MicrosoftSQL** **Server Stored ProcedureResolver** para **@value**.  
  
2.  Ejecute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, el valor **resolver_info** para **@property**y el nombre del procedimiento almacenado que implementa la lógica de solucionador de conflictos para **@value**.  
  
##  <a name="COM"></a> Usar un solucionador personalizado basado en COM  
 El espacio de nombres <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> implementa una interfaz que le permite escribir una lógica de negocios compleja para administrar eventos y solucionar conflictos que se producen durante el proceso de sincronización de replicación de mezcla. Para más información, consulte [Implement a Business Logic Handler for a Merge Article](implement-a-business-logic-handler-for-a-merge-article.md). También puede escribir su propia lógica de negocios personalizada basada en código nativo para solucionar conflictos. Esta lógica está generada como componente COM y se compila en las bibliotecas de vínculo dinámico (DLL), usando productos como [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++. Este solucionador de conflictos personalizado basado en COM debe implementar la interfaz **ICustomResolver** , que está diseñada específicamente para la resolución de conflictos.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>Para crear y registrar un solucionador de conflictos personalizado basado en COM  
  
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
  
8.  En el Publicador, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) para comprobar que la biblioteca no está registrada aún como solucionador de conflictos personalizado.  
  
9. Para registrar la biblioteca como solucionador de conflictos personalizado, ejecute [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql) en el Distribuidor. Especifique el nombre descriptivo del objeto COM para **@article_resolver**, Id. (CLSID de la biblioteca) para **@resolver_clsid**y un valor de `false` para **@is_dotnet_assembly**.  
  
    > [!NOTE]  
    >  Cuando ya no se necesite, se puede eliminar del registro un solucionador de conflictos personalizado usando [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql).  
  
10. (Opcional) En un clúster, repita los pasos 5-8 para registrar el solucionador personalizado en todos los nodos del clúster. Esto es necesario para asegurar que el solucionador personalizado pueda cargar correctamente la reconciliación tras una conmutación por error.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>Para utilizar un solucionador de conflictos personalizado con un nuevo artículo de tabla  
  
1.  En el Publicador, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) y tenga en cuenta el nombre descriptivo del solucionador que desee.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir un artículo. Especifique el nombre descriptivo del solucionador de artículos del paso 1 para **@article_resolver**. Para más información, consulte [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>Para utilizar un solucionador de conflictos personalizado con un artículo de tabla existente  
  
1.  En el Publicador, ejecute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) y tenga en cuenta el nombre descriptivo del solucionador que desee.  
  
2.  Ejecute [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) especificando **@publication**, **@article** un valor de **article_resolver** para **@property** y el nombre descriptivo del solucionador de artículos del paso 1 para **@value**.  
  
#### <a name="viewing-a-sample-custom-resolver"></a>Ver un solucionador personalizado de ejemplo  
  
1.  Hay un ejemplo disponible en los archivos de ejemplo de SQL Server 2000. Descargue el archivo **sql2000samples.cab** desde [Ejemplos actualizados para SQL Server 2000 Service Pack 3](http://www.microsoft.com/download/details.aspx?id=8560). Se descargan 8 archivos que ocupan 6,9 MB.  
  
2.  Extraiga los archivos del archivo comprimido .cab descargado.  
  
3.  Ejecute **setup.exe**.  
  
    > [!NOTE]  
    >  Al elegir las opciones de instalación, solo es necesario instalar los ejemplos de **Replicación** . (La ruta de instalación predeterminada es **C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\\**)  
  
4.  Vaya a la carpeta de instalación. (La carpeta predeterminada es **C:\Archivos de programa (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**).  
  
5.  Ejecute el programa **unzip_sqlreplSP3.exe** .  
  
    > [!NOTE]  
    >  El solucionador com de ejemplo se instalará de forma predeterminada en la carpeta **C:\Archivos de programa (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** .  
  
6.  En la carpeta **subspres** , busque todas las repeticiones de **#include sqlres.h** en todos los archivos de origen y reemplácelas con **#import "replrec.dll" no_namespace, raw_interfaces_only**.  
  
## <a name="see-also"></a>Vea también  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM-Based Custom Resolvers](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md)  
  
  
