---
title: Roles fijos de base de datos del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a8067aaa2133648c1a1ea4fff81db08c139d5278
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67793404"
---
# <a name="sql-server-agent-fixed-database-roles"></a>Roles fijos de base de datos del Agente SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene los siguientes roles fijos de base de datos de la base de datos **msdb**, que proporcionan a los administradores un control más preciso a la hora de obtener acceso al Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los roles enumerados de menor a mayor privilegio de acceso son:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Cuando los usuarios que no son miembros de uno de estos roles se conectan con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el nodo del **Agente SQL Server** no está visible en el Explorador de objetos. Es preciso que los usuarios sean miembros de los roles fijos de base de datos o del rol fijo de servidor **sysadmin** para poder usar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Permisos de los roles fijos de base de datos del Agente SQL Server  
 Los permisos de los roles de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son concéntricos: los roles con más privilegios heredan los permisos de los roles con menos privilegios en los objetos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (incluidos alertas, operadores, trabajos, programaciones y servidores proxy). Por ejemplo, si los miembros del rol **SQLAgentUserRole** con menos privilegios reciben acceso al proxy_A, los miembros del rol **SQLAgentReaderRole** y del rol **SQLAgentOperatorRole** automáticamente tendrán acceso a este proxy incluso si no se les concedió explícitamente el acceso al proxy_A. Esto puede tener implicaciones de seguridad, que se describen en las siguientes secciones sobre cada rol.  
  
### <a name="sqlagentuserrole-permissions"></a>Permisos de SQLAgentUserRole  
 **SQLAgentUserRole** es el rol con menos privilegios de todos los roles fijos de la base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Solo dispone de permisos para operadores, trabajos locales y programaciones de trabajos. Los miembros de **SQLAgentUserRole** solo tienen permisos en los trabajos locales y en las programaciones de trabajos que les pertenecen. No pueden utilizar trabajos multiservidor (trabajos de servidor de destino y de servidor principal), ni pueden cambiar la propiedad de un trabajo para obtener acceso a trabajos que todavía no les pertenecen. Los miembros de**SQLAgentUserRole** pueden ver una lista de los servidores proxy disponibles únicamente en el cuadro de diálogo **Propiedades de paso de trabajo** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para los miembros de **SQLAgentUserRole** solo está visible el nodo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Trabajos **del Explorador de objetos de**.  
  
> [!IMPORTANT]  
>  Tenga en cuenta las implicaciones de seguridad antes de conceder acceso de proxy **a los miembros de**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles**. Los roles **SQLAgentReaderRole** y **SQLAgentOperatorRole** se convierten automáticamente en miembros del rol **SQLAgentUserRole**. Esto significa que los miembros de los roles **SQLAgentReaderRole** y **SQLAgentOperatorRole** tienen acceso a todos los servidores proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo acceso se concedió a **SQLAgentUserRole** y, por tanto, pueden utilizar dichos servidores proxy.  
  
 En la siguiente tabla encontrará un resumen de los permisos del rol **SQLAgentUserRole** para los objetos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Acción|Operadores|Trabajos locales<br /><br /> (solo trabajos que les pertenecen)|Programación de trabajos<br /><br /> (solo programaciones que les pertenecen)|Servidores proxy|  
|------------|---------------|----------------------------------------|------------------------------------------------|-------------|  
|Crear, modificar o eliminar|No|Sí <sup>1</sup>|Sí|No|  
|Ver lista (enumerar)|Sí <sup>2</sup>|Sí|Sí|Sí <sup>3</sup>|  
|Habilitar o deshabilitar|No|Sí|Sí|No aplicable|  
|Ver propiedades|No|Sí|Sí|No|  
|Ejecutar, detener o iniciar|No aplicable|Sí|No aplicable|No aplicable|  
|Ver historial de trabajos|No aplicable|Sí|No aplicable|No aplicable|  
|Eliminar historial de trabajos|No aplicable|No <sup>4</sup>|No aplicable|No aplicable|  
|Adjuntar o separar|No aplicable|No aplicable|Sí|No aplicable|  
  
 <sup>1</sup> no se puede cambiar la propiedad del trabajo.  
  
 <sup>2</sup> puede obtener una lista de operadores disponibles para su uso en **sp_notify_operator** y en el cuadro de diálogo **propiedades del trabajo** de Management Studio.  
  
 <sup>3</sup> la lista de servidores proxy solo está disponible en el cuadro de diálogo **propiedades de paso de trabajo** de Management Studio.  
  
 <sup>4</sup> a los miembros de **SQLAgentUserRole** se les debe conceder EXPLÍCITAmente el permiso Execute en **sp_purge_jobhistory** para eliminar el historial de trabajos de los trabajos que les pertenecen. No pueden eliminar el historial de ningún otro trabajo.  
  
### <a name="sqlagentreaderrole-permissions"></a>Permisos de SQLAgentReaderRole  
 El rol**SQLAgentReaderRole** incluye todos los permisos de **SQLAgentUserRole** , así como también los permisos para ver la lista de trabajos multiservidor disponibles, sus propiedades y su historial. Los miembros de este rol también pueden ver la lista de trabajos y programaciones de trabajos disponibles y sus propiedades, y no solo los trabajos y programaciones de trabajos que les pertenecen. Los miembros del rol**SQLAgentReaderRole** no pueden cambiar la propiedad de un trabajo para obtener acceso a trabajos que ya no les pertenecen. Para los miembros del rol **SQLAgentReaderRole** , solo está visible el nodo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Trabajos **del Explorador de objetos de**.  
  
> [!IMPORTANT]  
>  Tenga en cuenta las implicaciones de seguridad antes de conceder acceso de proxy **a los miembros de**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles**. Los miembros del rol **SQLAgentReaderRole** se convierten inmediatamente en miembros del rol **SQLAgentUserRole**. Esto significa que los miembros del rol **SQLAgentReaderRole** tienen acceso a todos los servidores proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo acceso se concedió a **SQLAgentUserRole** y, por tanto, pueden usar dichos servidores proxy.  
  
 En la tabla siguiente encontrará un resumen de los permisos de **SQLAgentReaderRole** para los objetos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Acción|Operadores|Trabajos locales|Trabajos multiservidor|Programación de trabajos|Servidores proxy|  
|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Crear, modificar o eliminar|No|Sí <sup>1</sup> (solo trabajos de propiedad)|No|Sí (solo programaciones que les pertenecen)|No|  
|Ver lista (enumerar)|Sí <sup>2</sup>|Sí|Sí|Sí|Sí <sup>3</sup>|  
|Habilitar o deshabilitar|No|Sí (solo trabajos que les pertenecen)|No|Sí (solo programaciones que les pertenecen)|No aplicable|  
|Ver propiedades|No|Sí|Sí|Sí|No|  
|Modificar propiedades|No|Sí (solo trabajos que les pertenecen)|No|Sí (solo programaciones que les pertenecen)|No|  
|Ejecutar, detener o iniciar|No aplicable|Sí (solo trabajos que les pertenecen)|No|No aplicable|No aplicable|  
|Ver historial de trabajos|No aplicable|Sí|Sí|No aplicable|No aplicable|  
|Eliminar historial de trabajos|No aplicable|No <sup>4</sup>|No|No aplicable|No aplicable|  
|Adjuntar o separar|No aplicable|No aplicable|No aplicable|Sí (solo programaciones que les pertenecen)|No aplicable|  
  
 <sup>1</sup> no se puede cambiar la propiedad del trabajo.  
  
 <sup>2</sup> puede obtener una lista de operadores disponibles para su uso en **sp_notify_operator** y en el cuadro de diálogo **propiedades del trabajo** de Management Studio.  
  
 <sup>3</sup> la lista de servidores proxy solo está disponible en el cuadro de diálogo **propiedades de paso de trabajo** de Management Studio.  
  
 <sup>4</sup> a los miembros de **SQLAgentReaderRole** se les debe conceder EXPLÍCITAmente el permiso Execute en **sp_purge_jobhistory** para eliminar el historial de trabajos de los trabajos que les pertenecen. No pueden eliminar el historial de ningún otro trabajo.  
  
### <a name="sqlagentoperatorrole-permissions"></a>Permisos de SQLAgentOperatorRole  
 **SQLAgentOperatorRole** es el rol con más privilegios de todos los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Incluye todos los permisos de los roles **SQLAgentUserRole** y **SQLAgentReaderRole**. Los miembros de este rol también pueden ver las propiedades de operadores y servidores proxy, así como enumerar los servidores proxy y alertas disponibles en el servidor.  
  
 Los miembros del rol**SQLAgentOperatorRole** tienen permisos adicionales en las programaciones y los trabajos locales. Pueden ejecutar, detener o iniciar todos los trabajos locales, y pueden eliminar el historial de trabajos de cualquier trabajo local del servidor. También pueden habilitar o deshabilitar todos los trabajos locales y programaciones del servidor. Para habilitar o deshabilitar programaciones o trabajos locales, los miembros de este rol deben usar los procedimientos almacenados **sp_update_job** y **sp_update_schedule**. Solo los miembros de **SQLAgentOperatorRole**pueden especificar los parámetros que especifican el nombre o el identificador del trabajo o la programación y el ** \@parámetro habilitado** . Si especifican cualquier otro parámetro, se producirá un error en la ejecución de estos procedimientos almacenados. Los miembros de**SQLAgentOperatorRole** no pueden cambiar la propiedad de un trabajo para obtener acceso a trabajos que ya no les pertenecen.  
  
 Para los miembros del rol **SQLAgentOperatorRole**, están visibles los nodos **Trabajos**, **Alertas**, **Operadores** y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Servidores proxy **del Explorador de objetos de**. El único nodo que no está visible para los miembros de este rol es el nodo **Registros de errores** .  
  
> [!IMPORTANT]  
>  Tenga en cuenta las implicaciones de seguridad antes de conceder acceso de proxy **a los miembros de**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles**. Los miembros del rol **SQLAgentOperatorRole** se convierten automáticamente en miembros de los roles **SQLAgentUserRole** y **SQLAgentReaderRole**. Esto significa que los miembros del rol **SQLAgentOperatorRole** tienen acceso a todos los servidores proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo acceso se concedió a **SQLAgentUserRole** o **SQLAgentReaderRole** y, por tanto, pueden usar dichos servidores proxy.  
  
 En la siguiente tabla encontrará un resumen de los permisos de **SQLAgentOperatorRole** para los objetos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Acción|Alertas|Operadores|Trabajos locales|Trabajos multiservidor|Programación de trabajos|Servidores proxy|  
|------------|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Crear, modificar o eliminar|Sin|No|Sí <sup>2</sup> (solo trabajos de propiedad)|No|Sí (solo programaciones que les pertenecen)|No|  
|Ver lista (enumerar)|Sí|Sí <sup>1</sup>|Sí|Sí|Sí|Sí|  
|Habilitar o deshabilitar|Sin|No|Sí <sup>3</sup>|No|Sí <sup>4</sup>|No aplicable|  
|Ver propiedades|Sí|Sí|Sí|Sí|Sí|Sí|  
|Modificar propiedades|Sin|No|Sí (solo trabajos que les pertenecen)|No|Sí (solo programaciones que les pertenecen)|No|  
|Ejecutar, detener o iniciar|No aplicable|No aplicable|Sí|No|No aplicable|No aplicable|  
|Ver historial de trabajos|No aplicable|No aplicable|Sí|Sí|No aplicable|No aplicable|  
|Eliminar historial de trabajos|No aplicable|No aplicable|Sí|No|No aplicable|No aplicable|  
|Adjuntar o separar|No aplicable|No aplicable|No aplicable|No aplicable|Sí (solo programaciones que les pertenecen)|No aplicable|  
  
 <sup>1</sup> puede obtener una lista de operadores disponibles para su uso en **sp_notify_operator** y en el cuadro de diálogo **propiedades del trabajo** de Management Studio.  
  
 <sup>2</sup> no se puede cambiar la propiedad del trabajo.  
  
 <sup>3</sup> los miembros de **SQLAgentOperatorRole** pueden habilitar o deshabilitar trabajos locales que no son de su propiedad mediante el procedimiento almacenado **sp_update_job** y especificando valores para los ** \@parámetros habilitados** y ** \@job_id** (o ** \@job_name**). Si un miembro de este rol especifica cualquier otro parámetro para este procedimiento almacenado, la ejecución del procedimiento producirá un error.  
  
 <sup>4</sup> los miembros de **SQLAgentOperatorRole** pueden habilitar o deshabilitar las programaciones que no les pertenecen mediante el procedimiento almacenado **sp_update_schedule** y especificar valores para los ** \@parámetros habilitados** y ** \@schedule_id** (o ** \@nombre**). Si un miembro de este rol especifica cualquier otro parámetro para este procedimiento almacenado, la ejecución del procedimiento producirá un error.  
  
## <a name="assigning-users-multiple-roles"></a>Asignar a los usuarios varios roles  
 Los miembros del rol fijo de servidor **sysadmin** tienen acceso a toda la funcionalidad del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si un usuario no es miembro del rol **sysadmin** , pero sí lo es de más de un rol fijo de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , es importante recordar el modelo de permisos concéntricos de estos roles. Debido a que los roles con más privilegios siempre contienen todos los permisos de los roles con menos privilegios, un usuario que sea miembro de más de un rol automáticamente tendrá los permisos asociados con el rol con más privilegios del que sea miembro.  
  
## <a name="see-also"></a>Consulte también  
 [Implementar la seguridad de Agente SQL Server](implement-sql-server-agent-security.md)   
 [sp_update_job &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)   
 [sp_update_schedule &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)   
 [sp_notify_operator &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)   
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)  
  
  
