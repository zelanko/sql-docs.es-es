---
title: SQL Server Audit (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- SQL Server Audit
- audits [SQL Server], SQL Server Audit
ms.assetid: 0c1fca2e-f22b-4fe8-806f-c87806664f00
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2f4f291e5dc4aaa8a240757713cc65bd2a6a8230
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055493"
---
# <a name="sql-server-audit-database-engine"></a>SQL Server Audit (motor de base de datos)
  La*auditoría* de una instancia de [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] o de una base de datos individual implica el seguimiento y registro de los eventos que se producen en [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. La auditoría de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite crear auditorías de servidor, que pueden contener especificaciones de auditoría de servidor para los eventos de servidor, y especificaciones de auditoría de base de datos para los eventos de base de datos. Los eventos auditados se pueden escribir en los registros de eventos o en los archivos de auditoría.  
  
 Hay varios niveles de auditoría disponibles para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], dependiendo de los requisitos gubernamentales o normativos de cada instalación. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit proporciona las herramientas y los procesos necesarios para habilitar, almacenar y ver auditorías en varios objetos de servidor y de base de datos.  
  
 Puede registrar grupos de acciones de auditoría en el servidor por instancia, así como grupos de acciones o acciones de auditoría en la base de datos por base de datos. El evento de auditoría se producirá cada vez que se encuentre la acción auditable.  
  
 Todas las ediciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admiten auditorías en el nivel de servidor. Las auditorías de nivel de base de datos se limitan a las ediciones Enterprise, Developer y Evaluation. Para obtener más información, vea [características compatibles con las ediciones de SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="sql-server-audit-components"></a>Componentes de SQL Server Audit  
 Una *auditoría* es la combinación de varios elementos en un único paquete para un grupo específico de acciones de servidor o de base de datos. Los componentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit se combinan para producir una salida denominada auditoría, de la misma manera que una definición de informe combinada con gráficos y elementos de datos da como resultado un informe.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit usa *eventos extendidos* para facilitar la creación de auditorías. Para obtener más información sobre los eventos extendidos, vea [eventos extendidos](../../extended-events/extended-events.md).  
  
### <a name="sql-server-audit"></a>SQL Server Audit  
 El objeto *SQL Server Audit* recopila una única instancia de acciones de nivel de base de datos o de servidor, así como grupos de acciones que se van a supervisar. La auditoría se realiza en el nivel de instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Es posible tener varias auditorías por cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Cuando se define una auditoría, se especifica la ubicación para los resultados generados. Éste es el destino de la auditoría. La auditoría se crea en un estado *deshabilitado* y no audita automáticamente ninguna acción. Una vez habilitada la auditoría, el destino de la auditoría recibe los datos de la misma.  
  
### <a name="server-audit-specification"></a>Especificación de auditoría de servidor  
 El objeto *Especificación de auditoría de servidor* pertenece a una auditoría. Puede crear una especificación de auditoría de servidor por cada auditoría, ya que ambos se crean en el ámbito de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 La especificación de auditoría de servidor recopila muchos grupos de acciones de nivel de servidor generados por la característica Extended Events. Puede incluir *grupos de acciones de auditoría* en una especificación de auditoría de servidor. Los grupos de acciones de auditoría son grupos predefinidos de acciones, que constituyen eventos atómicos que tienen lugar en el [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Estas acciones se envían a la auditoría, que las registra en el destino.  
  
 Los grupos de acciones de auditoría de nivel de servidor se describen en el tema [Grupos de acciones y acciones de SQL Server Audit](sql-server-audit-action-groups-and-actions.md).  
  
### <a name="database-audit-specification"></a>Especificación de auditoría de base de datos  
 El objeto *Especificación de auditoría de base de datos* también pertenece a una auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Puede crear una única especificación de auditoría de base de datos para cada base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y cada auditoría.  
  
 La especificación de auditoría de base de datos recopila acciones de auditoría de nivel de base de datos generadas por la característica Extended Events. Puede agregar grupos de acciones de auditoría o eventos de auditoría a una especificación de auditoría de base de datos. Los*eventos de auditoría* son las acciones atómicas que puede auditar el motor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Los*grupos de acciones de auditoría* son grupos predefinidos de acciones. Ambos están en el ámbito de la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Estas acciones se envían a la auditoría, que las registra en el destino. No incluya objetos con ámbito en el servidor, como las vistas del sistema, en una especificación de auditoría de base de datos.  
  
 Los grupos de acciones de auditoría de base de datos y las acciones de auditoría se describen en el tema [Grupos de acciones y acciones de SQL Server Audit](sql-server-audit-action-groups-and-actions.md).  
  
### <a name="target"></a>Destino  
 Los resultados de una auditoría se envían a un destino, que puede ser un archivo, el registro de eventos de seguridad de Windows o el registro de eventos de aplicación Windows. Los registros se deben revisar y archivar periódicamente para garantizar que el destino tiene espacio suficiente para escribir registros adicionales.  
  
> [!IMPORTANT]  
>  Cualquier usuario autenticado puede leer y escribir en el registro de eventos de aplicación Windows. El registro de eventos de aplicación requiere permisos más bajos que el registro de eventos de seguridad de Windows, por lo que es menos seguro que éste.  
  
 La escritura en el registro de seguridad de Windows requiere que se agregue la cuenta del servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la directiva **Generar auditorías de seguridad** . De forma predeterminada, el sistema local, el servicio local y el servicio de red forman parte de esta directiva. Este valor se puede configurar utilizando el complemento de directiva de seguridad (secpol.msc). Además, la directiva de seguridad **Auditar el acceso a objetos** debe estar habilitada tanto para **Correcto** como para **Error**. Este valor se puede configurar utilizando el complemento de directiva de seguridad (secpol.msc). En [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] o Windows Server 2008, puede establecer la Directiva de aplicación más granular **generada** desde la línea de comandos mediante el programa de directiva de auditoría ( `AuditPol.exe)` . Para obtener más información sobre los pasos necesarios para habilitar la escritura en el registro de seguridad de Windows, vea [Escribir eventos de auditoría de SQL Server en el registro de seguridad](write-sql-server-audit-events-to-the-security-log.md). Para obtener más información sobre el programa Auditpol.exe, vea el artículo 921469 de Knowledge Base que describe [cómo usar la directiva de grupo para configurar las opciones detalladas de auditoría de seguridad](https://support.microsoft.com/kb/921469/). Los registros de eventos de Windows son globales para el sistema operativo Windows. Para obtener más información sobre los registros de eventos de Windows, vea [Información general sobre el Visor de eventos](https://go.microsoft.com/fwlink/?LinkId=101455). Si necesita permisos más concretos en la auditoría, utilice el destino de archivo binario.  
  
 Al guardar información de auditoría en un archivo, para tratar de impedir su alteración, puede restringir el acceso a la ubicación del archivo de las maneras siguientes:  
  
-   La cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe tener los permisos de lectura y escritura.  
  
-   Normalmente, los administradores de auditoría requieren los permisos de lectura y escritura. Entonces, se supone que los administradores de auditoría son cuentas de Windows para la administración de archivos de auditoría, por ejemplo para la copia en diversos recursos compartidos, la copia de seguridad, etc.  
  
-   Los lectores de auditoría autorizados para leer archivos de auditoría deben tener permiso de lectura.  
  
 Incluso cuando el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] está escribiendo en un archivo, otros usuarios de Windows pueden leer el archivo de auditoría si tienen permiso. El [!INCLUDE[ssDE](../../../includes/ssde-md.md)] no crea ningún bloqueo exclusivo que evite las operaciones de lectura.  
  
 Dado que el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] puede tener acceso al archivo, los inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que tengan el permiso CONTROL SERVER pueden utilizar el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para tener acceso a los archivos de auditoría. Para registrar a todos los usuarios que estén leyendo el archivo de auditoría, defina una auditoría en master.sys.fn_get_audit_file. De esta forma se registran los inicios de sesión con permiso CONTROL SERVER que hayan tenido acceso al archivo de auditoría a través de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Si un administrador de auditoría copia el archivo en otra ubicación (para archivarlo, etc.), los permisos de las ACL de la nueva ubicación se deben reducir solo a los siguientes:  
  
-   Administrador de auditoría: lectura/escritura  
  
-   Lector de auditoría: lectura  
  
 Es recomendable generar los informes de la auditoría desde otra instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], por ejemplo una instancia de [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)]a la que solo tengan acceso administradores de auditoría o lectores de auditoría. El uso de otra instancia de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para la creación de informes puede contribuir a evitar que usuarios no autorizados obtengan acceso al registro de la auditoría.  
  
 Puede proporcionar más protección contra el acceso no autorizado mediante el cifrado de la carpeta en que el archivo de la auditoría está almacenado. Para ello, puede utilizar el Cifrado de unidad Bitlocker de Windows o el Sistema de archivos de cifrado de Windows.  
  
 Para obtener más información sobre los registros de auditoría que se escriben en el destino, vea [SQL Server Audit Records](sql-server-audit-records.md).  
  
## <a name="overview-of-using-sql-server-audit"></a>Información general sobre el uso de SQL Server Audit  
 Puede utilizar [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)] para definir una auditoría. Una vez creada y habilitada la auditoría, el destino comenzará a recibir entradas.  
  
 Puede leer los registros de eventos de Windows mediante la utilidad **Visor de eventos** en Windows. Para los destinos de archivo, puede usar tanto el **Visor del archivo de registros** en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] como la función [fn_get_audit_file](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql) para leer el archivo de destino.  
  
 El proceso general de creación y uso de una auditoría es el siguiente:  
  
1.  Cree una auditoría y defina el destino.  
  
2.  Cree una especificación de auditoría de servidor o una especificación de auditoría de base de datos que se asigne a la auditoría. Habilite la especificación de auditoría.  
  
3.  Habilite la auditoría.  
  
4.  Lea los eventos de auditoría mediante el **Visor de eventos**de Windows, el **Visor del archivo de registros**o la función fn_get_audit_file.  
  
 Para obtener más información, consulte [Crear una auditoría de servidor y una especificación de auditoría de servidor](create-a-server-audit-and-server-audit-specification.md) y [Crear una especificación de auditoría de servidor y de auditoría de base de datos](create-a-server-audit-and-database-audit-specification.md).  
  
## <a name="considerations"></a>Consideraciones  
 Si se produce un error al comenzar la auditoría, el servidor no se iniciará. En este caso, el servidor se puede iniciar mediante la opción **-f** en la línea de comandos.  
  
 Si un error de auditoría hace que el servidor se cierre o no se inicie porque se ha especificado ON_FAILURE=SHUTDOWN para la auditoría, se escribirá en el registro el evento MSG_AUDIT_FORCED_SHUTDOWN. Dado que el apagado se producirá en la primera aparición de este valor, el evento se escribirá una vez. Este evento se escribirá después de la aparición del mensaje del error para la auditoría que ha provocado el cierre. El administrador puede omitir los cierres provocados por auditorías si inicia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en modo de usuario único mediante la marca **-m**. De esta forma, indicará al sistema que cualquier auditoría en la que se haya especificado ON_FAILURE=SHUTDOWN debe ejecutarse en esa sesión como ON_FAILURE=CONTINUE. Cuando se inicia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con la marca **-m**, se escribe el mensaje MSG_AUDIT_SHUTDOWN_BYPASSED en el registro de errores.  
  
 Para obtener más información sobre las opciones de inicio del servicio, vea [Opciones de inicio del servicio de motor de base de datos](../../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
### <a name="attaching-a-database-with-an-audit-defined"></a>Adjuntar una base de datos con una auditoría definida  
 Si se adjunta una base de datos que tiene una especificación de auditoría y que especifica un GUID que no existe en el servidor, se producirá una especificación de auditoría *huérfana* . Dado que en la instancia del servidor no existe ninguna auditoría con ese GUID, no se grabará ningún evento de auditoría. Para corregir esta situación, utilice el comando ALTER DATABASE AUDIT SPECIFICATION para conectar la especificación de auditoría huérfana a una auditoría de servidor existente. O bien use el comando CREATE SERVER AUDIT para crear una nueva auditoría de servidor con el GUID especificado.  
  
 Si lo desea, puede adjuntar una base de datos en la que se haya definido una especificación de auditoría a otra edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no admita [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit, como [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] , pero no se registrará ningún evento de auditoría.  
  
### <a name="database-mirroring-and-sql-server-audit"></a>Creación de reflejo de la base de datos y SQL Server Audit  
 Una base de datos en la que se haya definido una especificación de auditoría de base de datos y que use la creación de reflejo de la base de datos incluirá la especificación de auditoría de base de datos. Para poder trabajar correctamente en la instancia de SQL reflejada, se deben configurar los elementos siguientes:  
  
-   El servidor reflejado debe tener una auditoría con el mismo GUID para permitir que la especificación de auditoría de base de datos escriba registros de auditoría. Esto se puede configurar mediante el comando CREATE AUDIT WITH GUID `=` * \<GUID from source Server Audit*> .  
  
-   En el caso de los destinos de archivo binario, la cuenta de servicio del servidor reflejado debe tener los permisos adecuados para la ubicación en la que se escribe la pista de auditoría.  
  
-   Si el destino es el registro de eventos de Windows, la directiva de seguridad del equipo en el que está ubicado el servidor reflejado debe permitir el acceso de la cuenta de servicio al registro de eventos de seguridad o de la aplicación.  
  
### <a name="auditing-administrators"></a>Auditar a los administradores  
 Los miembros del `sysadmin` rol fijo de servidor se identifican como el usuario **DBO** en cada base de datos. Para auditar las acciones de los administradores, se auditan las acciones del usuario **dbo** .  
  
## <a name="creating-and-managing-audits-with-transact-sql"></a>Crear y administrar auditorías con Transact-SQL  
 Puede usar instrucciones DDL, vistas y funciones de administración dinámica y vistas de catálogo para implementar todos los aspectos de la Auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
### <a name="data-definition-language-statements"></a>Instrucciones de lenguaje de definición de datos (DDL)  
 Puede usar las siguientes instrucciones DDL para crear, modificar y quitar especificaciones de auditoría:  
  
|||  
|-|-|  
|[ALTER AUTHORIZATION](/sql/t-sql/statements/alter-authorization-transact-sql)|[CREATE SERVER AUDIT](/sql/t-sql/statements/create-server-audit-transact-sql)|  
|[ALTER DATABASE AUDIT SPECIFICATION](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)|[CREATE SERVER AUDIT SPECIFICATION](/sql/t-sql/statements/create-server-audit-specification-transact-sql)|  
|[ALTER SERVER AUDIT](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)|[DROP DATABASE AUDIT SPECIFICATION](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)|  
|[ALTER SERVER AUDIT SPECIFICATION](/sql/t-sql/statements/alter-server-audit-transact-sql)|[DROP SERVER AUDIT](/sql/t-sql/statements/drop-server-audit-transact-sql)|  
|[CREATE DATABASE AUDIT SPECIFICATION](/sql/t-sql/statements/create-database-audit-specification-transact-sql)|[DROP SERVER AUDIT SPECIFICATION](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)|  
  
### <a name="dynamic-views-and-functions"></a>Funciones y vistas dinámicas  
 En la tabla siguiente se enumeran las funciones y vistas dinámicas que puede usar con las auditorías de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Funciones y vistas dinámicas|Description|  
|---------------------------------|-----------------|  
|[sys.dm_audit_actions](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)|Devuelve una fila por cada acción de auditoría sobre la que se puede guardar información en el registro de auditoría y por cada grupo de acciones de auditoría que se puede configurar como parte de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit.|  
|[sys.dm_server_audit_status](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)|Proporciona información sobre el estado actual de la auditoría.|  
|[sys.dm_audit_class_type_map](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)|Devuelve una tabla que asigna el campo class_type del registro de auditoría al campo class_desc en sys.dm_audit_actions.|  
|[fn_get_audit_file](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)|Devuelve información de un archivo de auditoría creado por una auditoría de servidor.|  
  
### <a name="catalog-views"></a>Vistas de catálogo  
 En la tabla siguiente se enumeran las vistas de catálogo que puede usar con las auditorías de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Vistas de catálogo|Description|  
|-------------------|-----------------|  
|[sys.database_audit_specifications](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)|Contiene información sobre las especificaciones de auditoría de base de datos en una auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una instancia del servidor.|  
|[sys.database_audit_specification_details](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)|Contiene información sobre las especificaciones de auditoría de base de datos en una auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una instancia de servidor para todas las bases de datos.|  
|[sys.server_audits](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)|Contiene una fila para cada auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una instancia de servidor.|  
|[sys.server_audit_specifications](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)|Contiene información sobre las especificaciones de auditoría de servidor en una auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una instancia del servidor.|  
|[sys.server_audit_specifications_details](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)|Contiene información sobre los detalles de especificación de auditoría del servidor (acciones) en una auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una instancia de servidor.|  
|[sys.server_file_audits](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)|Contiene información adicional sobre el tipo de auditoría de archivos en una auditoría de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una instancia de servidor.|  
  
## <a name="permissions"></a>Permisos  
 Cada una de las características y los comandos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit tiene sus propios requisitos de permisos.  
  
 Para crear, modificar o quitar una auditoría de servidor o una especificación de auditoría de servidor, las entidades de seguridad de servidor requieren el permiso ALTER ANY SERVER AUDIT o CONTROL SERVER. Para crear, modificar o quitar una especificación de auditoría de base de datos, las entidades de seguridad de base de datos requieren el permiso ALTER ANY DATABASE AUDIT, o el permiso ALTER o CONTROL en la base de datos. Además, las entidades de seguridad deben tener el permiso para conectarse a la base de datos o los permisos ALTER ANY SERVER AUDIT o CONTROL SERVER.  
  
 A menos que se especifique lo contrario, para que una entidad de seguridad pueda ver las vistas de catálogo debe cumplir una de las condiciones siguientes:  
  
-   Pertenencia al rol fijo de servidor sysadmin.  
  
-   El permiso CONTROL SERVER.  
  
-   El permiso VIEW SERVER STATE.  
  
-   El permiso ALTER ANY AUDIT.  
  
-   El permiso VIEW AUDIT STATE (solo da el acceso principal a la vista de catálogo sys.server_audits).  
  
 Una entidad de seguridad debe tener el permiso VIEW SERVER STATE o ALTER ANY AUDIT para utilizar las vistas de administración dinámica.  
  
 Para obtener más información sobre cómo conceder derechos y permisos, vea [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql).  
  
> [!CAUTION]  
>  De la misma forma que las entidades de seguridad del rol sysadmin pueden manipular cualquier componente de auditoría, las del rol db_owner pueden manipular las especificaciones de auditoría en una base de datos. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit comprobará si un inicio de sesión que crea o modifica una especificación de auditoría tiene al menos el permiso ALTER ANY DATABASE AUDIT. Sin embargo, no realiza ninguna validación al adjuntar una base de datos. Como norma, debería otorgar la misma confianza a las especificaciones de auditoría de base de datos que a las entidades de seguridad que tienen el rol sysadmin o db_owner.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Crear una auditoría de servidor y una especificación de auditoría de servidor](create-a-server-audit-and-server-audit-specification.md)  
  
 [Crear una especificación de auditoría de servidor y de auditoría de base de datos](create-a-server-audit-and-database-audit-specification.md)  
  
 [Ver un registro de SQL Server Audit](view-a-sql-server-audit-log.md)  
  
 [Escribir eventos de SQL Server Audit en el registro de seguridad](write-sql-server-audit-events-to-the-security-log.md)  
  
## <a name="topics-closely-related-to-auditing"></a>Temas estrechamente relacionados con la auditoría  
 [Propiedades del servidor &#40;página Seguridad&#41;](../../../database-engine/configure-windows/server-properties-security-page.md)  
 Explica cómo activar la auditoría de inicio de sesión para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los registros de auditoría se almacenan en el registro de aplicación de Windows.  
  
 [c2 audit mode (opción de configuración del servidor)](../../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)  
 Explica la compatibilidad de seguridad del modo auditoría C2 en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Categoría de eventos Auditoría de seguridad &#40;SQL Server Profiler&#41;](../../../relational-databases/event-classes/security-audit-event-category-sql-server-profiler.md)  
 Explica los eventos de auditoría que puede utilizar en [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Para más información, consulte [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md).  
  
 [Seguimiento de SQL](../../sql-trace/sql-trace.md)  
 Explica cómo puede usar el Seguimiento de SQL desde sus propias aplicaciones para crear seguimientos manualmente, en lugar de usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Profiler.  
  
 [Desencadenadores DDL](../../triggers/ddl-triggers.md)  
 Explica cómo puede usar los desencadenadores del Lenguaje de definición de datos (DDL) para realizar el seguimiento de los cambios en sus bases de datos.  
  
 [Microsoft TechNet: SQL Server TechCenter: Seguridad y protección de SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=101152)  
 Proporciona información actualizada sobre la seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server grupos de acciones y acciones de auditoría](sql-server-audit-action-groups-and-actions.md)   
 [SQL Server Audit Records](sql-server-audit-records.md)  
  
  
