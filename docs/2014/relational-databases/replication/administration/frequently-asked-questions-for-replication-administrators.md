---
title: Preguntas más frecuentes para administradores de replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- administering replication, frequently asked questions
- replication [SQL Server], administering
ms.assetid: 5a9e4ddf-3cb1-4baf-94d6-b80acca24f64
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 30058e297e22ed63a9e22a4755f22c4cc35ab213
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105165"
---
# <a name="frequently-asked-questions-for-replication-administrators"></a>Preguntas más frecuentes para administradores de replicación
  Las siguientes preguntas y respuestas proporcionan instrucciones sobre las diversas tareas que deben ejecutar los administradores de bases de datos replicadas.  
  
## <a name="configuring-replication"></a>Configurar la replicación  
  
### <a name="does-activity-need-to-be-stopped-on-a-database-when-it-is-published"></a>¿Es preciso detener la actividad en una base de datos cuando se publica?  
 No. La actividad puede continuar en la base de datos mientras se crea una publicación. Tenga en cuenta que producir una instantánea puede consumir muchos recursos, por lo que es mejor generar instantáneas durante los períodos de menor actividad de la base de datos (de manera predeterminada, se genera una instantánea cuando se completa el Asistente para nueva publicación).  
  
### <a name="are-tables-locked-during-snapshot-generation"></a>¿Están bloqueadas las tablas durante la generación de instantáneas?  
 La duración de los bloqueos depende del tipo de replicación utilizada.  
  
-   Para las publicaciones de combinación, el Agente de instantáneas no adopta ningún bloqueo.  
  
-   Para las publicaciones transaccionales, el Agente de instantáneas adopta de manera predeterminada bloqueos únicamente durante la fase inicial de la generación de instantáneas.  
  
-   Para las publicaciones de instantáneas, el Agente de instantáneas adopta bloqueos durante todo el proceso de generación de instantáneas.  
  
 Como los bloqueos impiden al resto de los usuarios actualizar las tablas, el Agente de instantáneas debe programarse para que se ejecute durante los períodos de baja actividad de la base de datos, especialmente para las publicaciones de instantáneas.  
  
### <a name="when-is-a-subscription-available-when-can-the-subscription-database-be-used"></a>¿Cuándo está disponible una suscripción? ¿Cuándo se puede utilizar la base de datos de suscripciones?  
 Una suscripción está disponible después de haber aplicado la instantánea a la base de datos de suscripciones. Aunque se puede obtener acceso a la base de datos de suscripciones con anterioridad, la base de datos no se debe utilizar hasta que se haya aplicado la instantánea. Utilice el Monitor de replicación para comprobar el estado de la aplicación y generación de instantáneas:  
  
-   El Agente de instantáneas genera la instantánea. Vea el estado de la generación de instantáneas en la pestaña **Agentes** de una publicación en el Monitor de replicación. Para obtener más información, vea [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   La instantánea la aplica el Agente de distribución o el Agente de mezcla. Vea el estado de la aplicación de instantáneas en la página **Agente de distribución** o **Agente de mezcla** del Monitor de replicación. Para obtener más información, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
### <a name="what-happens-if-the-snapshot-agent-has-not-completed-when-the-distribution-or-merge-agent-starts"></a>¿Qué ocurre si el Agente de instantáneas no se ha completado cuando se inician el Agente de distribución o el Agente de mezcla?  
 Esto no causa ningún error si el Agente de distribución o el Agente de mezcla se ejecutan al mismo tiempo que el Agente de instantáneas. No obstante, debe tener en cuenta lo siguiente:  
  
-   Si el Agente de distribución o el Agente de mezcla están configurados para ejecutarse de forma continua, el agente aplica la instantánea automáticamente una vez que el Agente de instantáneas finaliza.  
  
-   Si el Agente de distribución o el Agente de mezcla están configurados para ejecutarse según una programación o a petición, y no hay ninguna instantánea disponible cuando el agente se ejecuta, el agente se cerrará con un mensaje en el que se indica que la instantánea no está disponible todavía. Es preciso volver a ejecutar el agente para aplicar la instantánea una vez que el Agente de instantáneas ha finalizado. Para más información sobre cómo ejecutar los agentes, vea [Sincronizar una suscripción de inserción](../synchronize-a-push-subscription.md), [Sincronizar una suscripción de extracción](../synchronize-a-pull-subscription.md) y [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md).  
  
### <a name="should-i-script-my-replication-configuration"></a>¿Debo generar script para la configuración de replicación?  
 Sí. Generar script para la configuración de replicación es una parte fundamental de cualquier plan de recuperación de desastres en una topología de replicación. Para obtener más información sobre la generación de script, vea [Scripting Replication](../scripting-replication.md).  
  
### <a name="what-recovery-model-is-required-on-a-replicated-database"></a>¿Qué modelo de recuperación se necesita para una base de datos replicada?  
 Funciones de replicación que utilicen correctamente uno de los modelos de recuperación: simple, completa o por medio de registros de operaciones masivas. La replicación de mezcla hace un seguimiento de los cambios almacenando información en tablas de metadatos. La replicación transaccional realiza un seguimiento de los cambios marcando el registro de transacciones, pero el modelo de recuperación no afecta a este proceso de marcado.  
  
### <a name="why-does-replication-add-a-column-to-replicated-tables-will-it-be-removed-if-the-table-isnt-published"></a>¿Por qué la replicación agrega una columna a las tablas replicadas? ¿Se quitará si la tabla no se publica?  
 Para realizar un seguimiento de los cambios, la replicación de mezcla y la replicación transaccional con suscripciones de actualización en cola deben poder identificar de forma única cada fila de todas las tablas publicadas. Para realizar esta acción:  
  
-   La replicación de mezcla agrega la columna **rowguid** a todas las tablas, a menos que la tabla ya tenga una columna del tipo de datos **uniqueidentifier** con la propiedad **ROWGUIDCOL** definida (en cuyo caso se utiliza dicha columna). Si la tabla se quita de la publicación, la columna **rowguid** se elimina; si se ha utilizado una columna existente para realizar el seguimiento, la columna no se quita.  
  
-   Si una publicación transaccional admite suscripciones de actualización en cola, la replicación agrega la columna **msrepl_tran_version** a todas las tablas. Si la tabla se quita de la publicación, la columna **msrepl_tran_version** no se elimina.  
  
-   Un filtro no debe incluir la columna `rowguidcol` que usa la replicación para identificar filas. De forma predeterminada, es la columna agregada al configurar la replicación de mezcla y se denomina **rowguid**.  
  
### <a name="how-do-i-manage-constraints-on-published-tables"></a>¿Cómo se administran las restricciones en las tablas publicadas?  
 Existen varios aspectos que deben tenerse en cuenta en relación con las restricciones en las tablas publicadas:  
  
-   La replicación transaccional requiere una restricción de clave principal en cada tabla publicada. La replicación de mezcla no requiere clave principal, pero si existe alguna, debe replicarse. La replicación de instantáneas no requiere clave principal.  
  
-   De manera predeterminada, las restricciones de clave principal, los índices y las restricciones CHECK se replican en los suscriptores.  
  
-   La opción NOT FOR REPLICATION se especifica de manera predeterminada para las restricciones de clave externa y las restricciones CHECK; las restricciones se exigen para las operaciones de usuario, pero no para las operaciones de agente.  
  
 Para obtener información acerca de la configuración de las opciones de esquema que controlan si las restricciones se replican o no, vea [Specify Schema Options](../publish/specify-schema-options.md).  
  
### <a name="how-do-i-manage-identity-columns"></a>¿Cómo se administran las columnas de identidad?  
 La replicación proporciona administración automática de intervalos de identidad para las topologías de replicación que incluyen actualizaciones en el suscriptor. Para más información, vea [Replicar columnas de identidad](../publish/replicate-identity-columns.md).  
  
### <a name="can-the-same-objects-be-published-in-different-publications"></a>¿Se pueden publicar los mismos objetos en publicaciones diferentes?  
 Sí, pero con algunas limitaciones. Para más información, vea la sección sobre cómo publicar tablas en varias publicaciones en el tema [Publicar datos y objetos de base de datos](../publish/publish-data-and-database-objects.md).  
  
### <a name="can-multiple-publications-use-the-same-distribution-database"></a>¿Pueden varias publicaciones utilizar la misma base de datos de distribución?  
 Sí. No existen limitaciones al número de tipos de publicaciones que pueden utilizar la misma base de datos de distribución. Todas las publicaciones de un publicador determinado deben utilizar el mismo distribuidor y base de datos de distribución.  
  
 Si dispone de varias publicaciones, puede configurar varias bases de datos de distribución en el distribuidor para asegurarse de que los datos que pasan a través de cada una de ellas proceden de una sola publicación. Use el cuadro de diálogo **Propiedades del distribuidor** o [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql) para agregar una base de datos de distribución. Para más información sobre cómo obtener acceso a este cuadro de diálogo, vea [Ver y modificar las propiedades del distribuidor y del publicador](../view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="how-do-i-find-information-on-the-distributor-and-publisher-such-as-which-objects-in-a-database-are-published"></a>¿Cómo se busca información en el distribuidor y el publicador, por ejemplo qué objetos de una base de datos se publican?  
 Esta información está disponible a través de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y de una serie de procedimientos almacenados de replicación. Para más información, consulte [Distributor and Publisher Information Script](distributor-and-publisher-information-script.md).  
  
### <a name="does-replication-encrypt-data"></a>¿La replicación cifra los datos?  
 No. La replicación no cifra los datos almacenados en la base de datos o transferidos a través de la red. Para más información, vea la sección sobre cifrado en el tema [Información general de seguridad &#40;replicación&#41;](../security/security-overview-replication.md)  
  
### <a name="how-do-i-replicate-data-over-the-internet"></a>¿Cómo se replican datos a través de Internet?  
 Los datos se replican a través de Internet mediante:  
  
-   Una red privada virtual (VPN). Para más información, vea [Publicar datos a través de Internet mediante VPN](../publish-data-over-the-internet-using-vpn.md).  
  
-   La opción de sincronización web para replicación de mezcla. Para más información, consulte [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md).  
  
 Todos los tipos de replicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden replicar datos a través de VPN, pero tenga en cuenta la sincronización web si está utilizando replicación de mezcla.  
  
### <a name="does-replication-resume-if-a-connection-is-dropped"></a>¿Se reanuda la replicación si se quita una conexión?  
 Sí. El procesamiento de replicación se reanuda en el punto en el que se dejó cuando se quitó la conexión. Si está utilizando la replicación de mezcla a través de una red que no es confiable, considere la posibilidad de utilizar registros lógicos, con lo que se asegurará de que los cambios se procesen como una unidad. Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](../merge/group-changes-to-related-rows-with-logical-records.md).  
  
### <a name="does-replication-work-over-low-bandwidth-connections-does-it-use-compression"></a>¿Funciona la replicación a través de conexiones de poco ancho de banda? ¿Utiliza compresión?  
 Sí, la replicación funciona a través de conexiones de poco ancho de banda. En las conexiones sobre TCP/IP, utiliza la compresión proporcionada por el protocolo, pero no aporta compresión adicional. En las conexiones de sincronización web sobre HTTPS, utiliza la compresión proporcionada por el protocolo y también compresión adicional de los archivos XML utilizados para replicar cambios.  
  
## <a name="logins-and-object-ownership"></a>Inicios de sesión y propiedad de los objetos  
  
### <a name="are-logins-and-passwords-replicated"></a>¿Se replican las contraseñas y los inicios de sesión?  
 No. Puede crear un paquete DTS para transferir inicios de sesión y contraseñas de un publicador a uno o varios suscriptores.  
  
### <a name="what-are-schemas-and-how-are-they-replicated"></a>¿Qué esquemas se replican y cómo?  
 A partir de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], *esquema* tiene dos significados:  
  
-   La definición de un objeto, como una instrucción CREATE TABLE. De manera predeterminada, la replicación copia las definiciones de todos los objetos replicados en el suscriptor.  
  
-   El espacio de nombres dentro del que se crea un objeto: \<base de datos>.\<esquema>.\<objeto>. Los esquemas se definen mediante la instrucción CREATE SCHEMA.  
  
-   La replicación tiene el siguiente comportamiento predeterminado en el Asistente para nueva publicación con respecto a los esquemas y a la propiedad de objetos:  
  
-   Para artículos de publicaciones de combinación con un nivel de compatibilidad de 90 o superior, publicaciones de instantáneas y publicaciones transaccionales: de manera predeterminada, el propietario del objeto en el suscriptor es el mismo que el propietario del objeto correspondiente en el publicador. Si en el suscriptor no existen esquemas que posean objetos, se crean de forma automática.  
  
-   Para artículos en publicaciones de combinación con un nivel de compatibilidad menor de 90: de manera predeterminada, el propietario se deja en blanco y se especifica como **dbo** durante la creación del objeto en el suscriptor.  
  
-   Para artículos de publicaciones de Oracle: de forma predeterminada, el propietario se especifica como **dbo**.  
  
-   Para artículos de publicaciones que utilizan instantáneas en modo de carácter (que se utilizan para los que no son suscriptores de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y para los suscriptores de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ): de manera predeterminada, el propietario se deja en blanco. Como valor predeterminado del propietario se utiliza el propietario asociado con la cuenta utilizada por el Agente de distribución o el Agente de mezcla para conectarse con el suscriptor.  
  
 El propietario del objeto se puede cambiar mediante el cuadro de diálogo **Propiedades del artículo - \<***Artículo***>** y mediante los siguientes procedimientos almacenados: **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** y **sp_changemergearticle**. Para más información, vea [Ver y modificar propiedades de publicación](../publish/view-and-modify-publication-properties.md), [Definir un artículo](../publish/define-an-article.md) y [Ver y modificar las propiedades de un artículo](../publish/view-and-modify-article-properties.md).  
  
### <a name="how-can-grants-on-the-subscription-database-be-configured-to-match-grants-on-the-publication-database"></a>¿Cómo pueden configurarse las concesiones en la base de datos de suscripciones para que coincidan con las de la base de datos de publicaciones?  
 De manera predeterminada, la replicación no ejecuta instrucciones GRANT en la base de datos de suscripciones. Si desea que los permisos de la base de datos de suscripciones coincidan con los de la base de datos de publicaciones, utilice uno de los siguientes métodos:  
  
-   Ejecute instrucciones GRANT directamente en la base de datos de suscripciones.  
  
-   Utilice un script posterior a una instantánea para ejecutar las instrucciones. Para obtener más información, consulte [Ejecutar scripts antes y después de aplicar la instantánea](../execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Utilice el procedimiento almacenado [sp_addscriptexec](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql) para ejecutar las instrucciones.  
  
### <a name="what-happens-to-permissions-granted-in-a-subscription-database-if-a-subscription-is-reinitialized"></a>¿Qué ocurre con los permisos concedidos en una base de datos de suscripciones si se reinicializa la suscripción?  
 De manera predeterminada, los objetos del suscriptor se quitan y se vuelven a crear al reinicializar una suscripción, lo que provoca que todos los permisos concedidos para dichos objetos se quiten. Hay dos formas de controlar esto:  
  
-   Volver a aplicar las concesiones después de la reinicialización utilizando las técnicas descritas en la sección anterior.  
  
-   Especificar que los objetos no se quiten al reinicializar la suscripción. Antes de la reinicialización, elija entre:  
  
    -   Ejecute [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) o [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique un valor de 'pre_creation_cmd' (**sp_changearticle**) o 'pre_creation_command' (**sp_changemergearticle**) para el parámetro **@property** y un valor de 'none', 'delete' o 'truncate' para el parámetro **@value**.  
  
    -   En el cuadro de diálogo **Propiedades del artículo: \<Artículo>** de la sección **Objeto de destino**, seleccione un valor de **Mantener el objeto existente sin cambios**, **Eliminar datos. Si el artículo tiene un filtro de fila, elimine solo los datos que coincidan con el filtro.** o **Truncar todos los datos del objeto existente** para la opción **Acción si el nombre está en uso**. Para más información sobre el acceso a este cuadro de diálogo, vea [Ver y modificar propiedades de publicación](../publish/view-and-modify-publication-properties.md).  
  
## <a name="database-maintenance"></a>Mantenimiento de bases de datos  
  
### <a name="why-cant-i-run-truncate-table-on-a-published-table"></a>¿Por qué no se puede ejecutar TRUNCATE TABLE en una tabla publicada?  
 TRUNCATE TABLE es una operación no registrada que no activa desencadenadores. No está permitida porque la replicación no puede realizar el seguimiento de los cambios causados por la operación: la replicación transaccional realiza un seguimiento de los cambios a través del registro de transacciones; la replicación de mezcla realiza el seguimiento de los cambios mediante los desencadenadores de las tablas publicadas.  
  
### <a name="what-is-the-effect-of-running-a-bulk-insert-command-on-a-replicated-database"></a>¿Cuál es el efecto de ejecutar un comando de inserción masiva en una base de datos replicada?  
 Para la replicación transaccional se realiza el seguimiento de las inserciones masivas y se replican de la misma manera que otras inserciones. Para la replicación de mezcla, debe asegurarse de que los metadatos de seguimiento de cambios se actualizan adecuadamente.  
  
### <a name="are-there-any-replication-considerations-for-backup-and-restore"></a>¿Existe alguna consideración de replicación que deba tenerse en cuenta para copias de seguridad y restauración?  
 Sí. Hay una serie de consideraciones especiales para las bases de datos que participan en la replicación. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](back-up-and-restore-replicated-databases.md).  
  
### <a name="does-replication-affect-the-size-of-the-transaction-log"></a>¿Afecta la replicación al tamaño del registro de transacciones?  
 La replicación de mezcla y la replicación de instantáneas no afectan al tamaño del registro de transacciones, pero la replicación transaccional sí que puede afectar a dicho tamaño. Si una base de datos incluye una o varias publicaciones transaccionales, el registro no se trunca hasta que todas las transacciones relevantes para las publicaciones se hayan entregado en la base de datos de distribución. Si el registro de transacciones está aumentando demasiado y el Agente de registro del LOG se está ejecutando de forma programada, considere la posibilidad de acortar el intervalo entre ejecuciones. O establézcalo para que se ejecute en modalidad continua. Si está establecido para que se ejecute en modalidad continua (opción predeterminada), asegúrese de que se está ejecutando. Para más información sobre cómo comprobar el estado Agente de registro del LOG, vea [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 Además, si ha definido la opción 'sync with backup' en la base de datos de publicaciones o en la base de datos de distribución, el registro de transacciones no se trunca hasta que se ha realizado una copia de seguridad de todas las transacciones. Si el registro de transacciones está aumentando demasiado y ha definido esta opción, considere la posibilidad de acortar el intervalo entre las copias de seguridad de los registros de transacciones. Para más información, sobre cómo realizar copias de seguridad y restaurar bases de datos implicadas en la replicación transaccional, vea [Estrategias para hacer copias de seguridad y restaurar replicación de instantáneas o replicación transaccional](strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="how-do-i-rebuild-indexes-or-tables-in-replicated-databases"></a>¿Cómo se vuelven a generar índices o tablas en bases de datos replicadas?  
 Existen varios mecanismos para volver a generar índices. Todos ellos se pueden utilizar sin necesidad de tener en cuenta consideraciones especiales para replicación, con la siguiente excepción: las claves principales son necesarias en las tablas de las publicaciones transaccionales, por lo que no se pueden quitar y volver a crear claves principales en dichas tablas.  
  
### <a name="how-do-i-add-or-change-indexes-on-publication-and-subscription-databases"></a>¿Cómo se agregan o cambian índices en bases de datos de suscripciones y publicaciones?  
 Se pueden agregar índices en el publicador o los suscriptores sin consideraciones especiales en cuanto a replicación (tenga en cuenta que los índices pueden afectar al rendimiento). CREATE INDEX y ALTER INDEX no se replican, por lo que si agrega o cambia un índice, por ejemplo en el publicador, deberá realizar la misma adición o cambio en el suscriptor si desea que quede reflejado ahí.  
  
### <a name="how-do-i-move-or-rename-files-for-databases-involved-in-replication"></a>¿Cómo se mueven o cambian de nombre los archivos de las bases de datos que participan en la replicación?  
 En versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], mover o cambiar de nombre los archivos de base de datos exigía separar y volver a adjuntar la base de datos. Puesto que una base de datos replicada no se puede separar, la replicación tenía que quitarse de estas bases de datos primero. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se pueden mover o cambiar de nombre los archivos sin separar y volver a adjuntar la base de datos, sin efecto alguno en la replicación. Para más información sobre mover y cambiar el nombre de los archivos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
### <a name="how-do-i-drop-a-table-that-is-being-replicated"></a>¿Cómo se quita una tabla que se está replicando?  
 Primero, quite el artículo de la publicación mediante [sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql), [sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) o el cuadro de diálogo **Propiedades de la publicación: \<Publicación>**, y después quítelo de la base de datos mediante `DROP <Object>`. No se pueden quitar artículos de publicaciones transaccionales o de instantáneas después de que se hayan agregado suscripciones; es preciso quitar primero las suscripciones. Para más información, vea [Agregar y quitar artículos de publicaciones existentes](../publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="how-do-i-add-or-drop-columns-on-a-published-table"></a>¿Cómo se agregan o quitan columnas de una tabla publicada?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite una amplia variedad de cambios de esquema en objetos publicados, lo que incluye agregar y quitar columnas. Por ejemplo, ejecute ALTER TABLE... DROP COLUMN en el publicador y la instrucción se replica en los suscriptores y, a continuación, se ejecuta para quitar la columna. Los suscriptores que ejecutan versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] admiten agregar y quitar columnas a través de los procedimientos almacenados [sp_repladdcolumn](/sql/relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql) y [sp_repldropcolumn](/sql/relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql). Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="replication-maintenance"></a>Mantenimiento de la replicación  
  
### <a name="how-do-i-determine-if-the-data-at-subscribers-is-synchronized-with-data-at-the-publisher"></a>¿Cómo se determina si los datos de los suscriptores están sincronizados con los del publicador?  
 Utilice la validación. La validación informa de si un suscriptor determinado está sincronizado con el publicador. Para obtener más información, vea [Validar datos replicados](../validate-replicated-data.md). La validación no proporciona información acerca de qué filas no están sincronizadas correctamente, pero la utilidad [tablediff](../../../tools/tablediff-utility.md) sí.  
  
### <a name="how-do-i-add-a-table-to-an-existing-publication"></a>¿Cómo se agrega una tabla a una publicación existente?  
 Para agregar una tabla (u otro objeto), no es necesario detener la actividad en las bases de datos de publicaciones o suscripciones. Agregue una tabla a una publicación a través del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** o los procedimientos almacenados [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) y [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Para más información, vea [Agregar y quitar artículos de publicaciones existentes](../publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="how-do-i-remove-a-table-from-a-publication"></a>¿Cómo se quita una tabla de una publicación?  
 Quite una tabla de la publicación mediante [sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql), [sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) o el cuadro de diálogo **Propiedades de la publicación: \<Publicación>**. No se pueden quitar artículos de publicaciones transaccionales o de instantáneas después de que se hayan agregado suscripciones; es preciso quitar primero las suscripciones. Para más información, vea [Agregar y quitar artículos de publicaciones existentes](../publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### <a name="what-actions-require-subscriptions-to-be-reinitialized"></a>¿Qué acciones exigen que las suscripciones se reinicialicen?  
 Existen una serie de cambios de publicaciones y artículos que requieren que las suscripciones se reinicialicen. Para obtener más información, vea [Cambiar las propiedades de la publicación y de los artículos](../publish/change-publication-and-article-properties.md).  
  
### <a name="what-actions-cause-snapshots-to-be-invalidated"></a>¿Qué acciones provocan que las instantáneas se invaliden?  
 Existen una serie de cambios de publicaciones y artículos que invalidan las instantáneas y exigen que se generen otras nuevas. Para obtener más información, vea [Cambiar las propiedades de la publicación y de los artículos](../publish/change-publication-and-article-properties.md).  
  
### <a name="how-do-i-remove-replication"></a>¿Cómo se quita la replicación?  
 Las acciones necesarias para quitar la replicación de una base de datos dependen de si la base de datos tenía la función de base de datos de publicaciones, base de datos de suscripciones o ambas.  
  
### <a name="how-do-i-determine-whether-there-are-transactions-or-rows-to-be-replicated"></a>¿Cómo se determina si existen transacciones o filas para replicar?  
 Para la replicación transaccional, utilice procedimientos almacenados o la pestaña **Comandos sin distribuir** del Monitor de replicación. Para más información, vea [Ver comandos replicados y otra información en la base de datos de distribución &#40;programación de la replicación con Transact-SQL&#41](../monitor/view-replicated-commands-and-information-in-distribution-database.md) y [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
 Para la replicación de mezcla, utilice el procedimiento almacenado **sp_showpendingchanges**. Para más información, vea [sp_showpendingchanges &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql).  
  
### <a name="how-far-behind-is-the-distribution-agent-should-i-reinitialize"></a>¿Se ha quedado muy retrasado el Agente de distribución? ¿Debo reinicializarlo?  
 Utilice el procedimiento almacenado **sp_replmonitorsubscriptionpendingcmds** o la pestaña **Comandos sin distribuir** del Monitor de replicación. El procedimiento almacenado y la pestaña muestran lo siguiente:  
  
-   Número de comandos de la base de datos de distribución que no se han entregado al suscriptor seleccionado. Un comando se compone de una instrucción de lenguaje de manipulación de datos (DML) de Transact-SQL o una instrucción de lenguaje de definición de datos (DDL).  
  
-   Cantidad estimada de tiempo para entregar comandos al suscriptor. Si este valor es superior al tiempo necesario para generar y aplicar una instantánea en el suscriptor, considere la posibilidad de volver a reinicializar el suscriptor. Para obtener más información, vea [Reinicializar suscripciones](../reinitialize-subscriptions.md).  
  
 Para más información, vea [sp_replmonitorsubscriptionpendingcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql) y [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="replication-and-other-database-features"></a>Replicación y otras características de base de datos  
  
### <a name="does-replication-work-in-conjunction-with-log-shipping-and-database-mirroring"></a>¿Funciona la replicación junto con la creación de reflejo de la base de datos y el trasvase de registros?  
 Sí. Para más información, vea [Trasvase de registros y replicación &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md) y [Replicación y creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
### <a name="does-replication-work-in-conjunction-with-clustering"></a>¿Funciona la replicación junto con la agrupación en clústeres?  
 Sí. No tienen que tenerse en cuenta consideraciones especiales porque todos los datos se almacenan en un conjunto de discos en el clúster.  
  
## <a name="see-also"></a>Vea también  
 [Administración &#40;replicación&#41;](administration-replication.md)   
 [Best Practices for Replication Administration](best-practices-for-replication-administration.md)  
  
  
