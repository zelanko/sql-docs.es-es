---
title: "Propiedades de la base de datos (p&#225;gina Creaci&#243;n de reflejo) | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.databaseproperties.mirroring.f1"
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
caps.latest.revision: 86
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 86
---
# Propiedades de la base de datos (p&#225;gina Creaci&#243;n de reflejo)
  Acceda a esta página desde la base de datos principal y utilícela para configurar y modificar las propiedades de la creación de reflejo de una base de datos. Utilícela también para iniciar el Asistente para la configuración de seguridad de la creación de reflejo de bases de datos, ver el estado de una sesión de creación de reflejo y pausar o quitar la sesión de creación de reflejo de la base de datos.  
  
> **IMPORTANTE** La seguridad debe configurarse antes de empezar la creación del reflejo. Si la creación de reflejo no se ha iniciado, debe empezar con el asistente. Los cuadros de texto de la página **Creación de reflejo** se deshabilitan hasta que finalice el asistente.  
  
 **Configurar la creación de reflejo de la base de datos mediante SQL Server Management Studio**  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md)  
  
## Opciones  
 **Configurar seguridad**  
 Haga clic en este botón para ejecutar el **Asistente para la configuración de seguridad de la creación de reflejo de bases de datos**.  
  
 Si el asistente finaliza correctamente, la acción que realice dependerá de que la creación del reflejo haya empezado, de la forma siguiente:  
  
|||  
|-|-|  
|Si la creación del reflejo no ha empezado.|La página de propiedades almacena en caché la información de conexión, así como un valor que indica si la base de datos reflejada tiene el conjunto de propiedades asociadas.<br /><br /> Al final del asistente, se le pedirá que inicie la creación de reflejo de la base de datos mediante las direcciones de red del servidor predeterminadas y el modo de funcionamiento. Si necesita cambiar las direcciones o el modo de funcionamiento, haga clic en **No iniciar creación de reflejo**.|  
|Si la creación del reflejo ha empezado.|Si el servidor testigo se ha modificado en el asistente, se debe configurar en consecuencia.|  
  
 **Direcciones de red de servidor**  
 Existe una opción equivalente para cada instancia del servidor: **Principal**, **Reflejado** y **Testigo**.  
  
 Las direcciones de red de las instancias del servidor se especifican automáticamente cuando finalice el Asistente para la configuración de seguridad de la creación de reflejo de bases de datos. Una vez finalizado el asistente, puede modificar las direcciones de red manualmente, en caso necesario.  
  
 Las direcciones de red del servidor tienen la siguiente sintaxis básica:  
  
 TCP**://***fully_qualified_domain_name***:***port*  
  
 donde  
  
-   *fully_qualified_domain_name* es el servidor en el que existe la instancia del servidor.  
  
-   *puerto* es el puerto asignado al extremo de la creación de reflejo de la base de datos de la instancia del servidor.  
  
     Para participar en la creación de reflejo de la base de datos, un servidor requiere un extremo de la creación de reflejo de la base de datos. Si utiliza el Asistente para la configuración de seguridad de reflejo de bases de datos a fin de establecer la primera sesión de creación de reflejo para una instancia del servidor, el asistente crea automáticamente el extremo y lo configura para utilizar la autenticación de Windows. Para obtener información sobre cómo usar el asistente con la autenticación basada en certificados, vea [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md).  
  
    >**IMPORTANTE:**  Cada instancia del servidor requiere un extremo (solo uno) de creación de reflejo de la base de datos, independientemente del número de sesiones de creación de reflejo admitidas.  
  
 Por ejemplo, para una instancia del servidor en un equipo llamado `DBSERVER9` cuyo extremo utiliza el puerto `7022`, la dirección de red podría ser:  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 Para obtener más información, vea [Especificar una dirección de red de servidor &#40;creación de reflejo de la base de datos&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
> **NOTA:** Durante una sesión de creación de reflejo de la base de datos, las instancias del servidor principal y reflejado no pueden modificarse; sin embargo, la instancia del servidor testigo puede cambiarse durante una sesión. Para obtener más información, vea la sección "Notas" más adelante en este tema.  
  
 **Iniciar creación de reflejo**  
 Haga clic para iniciar la creación de reflejo, cuando se cumplan todas las condiciones siguientes:  
  
-   Debe existir la base de datos reflejada.  
  
     Antes de iniciar la creación del reflejo, debe haberse creado la base de datos reflejada mediante la restauración de una copia de seguridad reciente WITH NORECOVERY y, quizás, de las copias de seguridad de los registros de la base de datos principal en el servidor reflejado. Para obtener más información, vea [Preparar una base de datos reflejada para la creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
-   Las direcciones TCP de las instancias del servidor principal y reflejado ya están especificadas (en la sección **Direcciones de red de servidor**).  
  
-   Si el modo de funcionamiento está establecido en seguridad alta con conmutación automática por error (sincrónica), también se especifica la dirección TCP de la instancia del servidor reflejado.  
  
-   La seguridad se ha configurado correctamente.  
  
 Haga clic en **Iniciar creación de reflejo** para iniciar la sesión. El motor de base de datos intenta conectarse automáticamente al asociado de creación de reflejo para comprobar que el servidor reflejado esté configurado correctamente e iniciar la sesión de creación de reflejo. Si se puede iniciar la creación de reflejo, se crea un trabajo para supervisar la base de datos.  
  
 **Pausar** o **Reanudar**  
 Durante una sesión de creación de reflejo de la base de datos, haga clic en **Pausar** para poner en pausa la sesión. Aparecerá un mensaje de confirmación. Si hace clic en **Sí**, se pausará la sesión y el botón cambiará a **Reanudar**. Para reanudar la sesión, haga clic en **Reanudar**.  
  
 Para obtener más información sobre las repercusiones de pausar una sesión, vea [Pausar y reanudar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md).  
  
> **IMPORTANTE:** Después de un servicio forzado, si el servidor principal original se vuelve a conectar, se suspenderá la creación de reflejo. Reanudar la creación de reflejo en esta situación puede dar lugar a una pérdida de datos en el servidor principal original. Para obtener información sobre la administración de la posible pérdida de datos, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
 **Quitar creación de reflejo**  
 En la instancia del servidor principal, haga clic en esta opción para detener la sesión y quitar la configuración de creación de reflejo de las bases de datos. Aparecerá un mensaje para solicitar confirmación. Si hace clic en **Sí**se detendrá la sesión y se quitará la creación de reflejo. Para obtener más información sobre las repercusiones de quitar la creación de reflejo de la base de datos, vea [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
> **NOTA:** Si esta es la única base de datos reflejada de la instancia del servidor, el trabajo de supervisión se quitará.  
  
 **Conmutación por error**  
 Haga clic para conmutar por error manualmente la base de datos principal a la base de datos reflejada.  
  
> **NOTA:** Si la sesión de creación de reflejo se ejecuta en modo de rendimiento alto, la conmutación por error no se admite. Para conmutar por error manualmente, primero debe cambiar el modo de funcionamiento a **Seguridad alta sin conmutación automática por error (sincrónico)**. Una vez finalizada la conmutación por error, puede volver a cambiar el modo a **Rendimiento alto (asincrónico)** en la nueva instancia del servidor principal.  
  
 Aparecerá un mensaje de confirmación. Si hace clic en **Sí**, se intentará una conmutación por error. El servidor principal intenta conectarse al servidor reflejado mediante la Autenticación de Windows. Si la Autenticación de Windows no funciona, el servidor principal muestra el cuadro de diálogo **Conectar con el servidor** . Si el servidor reflejado usa la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , seleccione **Autenticación de SQL Server** en el cuadro **Autenticación** . En el cuadro de texto **Inicio de sesión** , especifique la cuenta de inicio de sesión para conectar con el servidor reflejado, y en el cuadro de texto **Contraseña** , especifique la contraseña correspondiente a la cuenta.  
  
 Si la conmutación por error se realiza correctamente, se cierra el cuadro de diálogo **Propiedades de la base de datos** . Los roles de los servidores principal y reflejado se intercambiarán: la anterior base de datos reflejada se convertirá en la base de datos principal, y viceversa. Observe que el cuadro de diálogo **Propiedades de la base de datos** no está disponible inmediatamente en la antigua base de datos principal, ya que se ha convertido en la base de datos reflejada; este cuadro de diálogo estará disponible en la nueva base de datos principal después de la conmutación por error.  
  
 Si no se puede efectuar la conmutación por error, aparece un mensaje de error y el cuadro de diálogo permanece abierto.  
  
> **IMPORTANTE:** Si hace clic en **Conmutación por error** después de modificar las propiedades en el cuadro de diálogo **Propiedades de la base de datos** , estos cambios se perderán. Para guardar los cambios actuales, responda **No** al mensaje de confirmación y haga clic en **Aceptar** para guardar los cambios. A continuación, vuelva a abrir el cuadro de diálogo de propiedades de la base de datos y haga clic en **Conmutación por error**.  
  
 **Modo de funcionamiento**  
 Opcionalmente, cambie el modo operativo. La disponibilidad de algunos modos operativos depende de si ha especificado una dirección TCP para un testigo. Las opciones son las siguientes:  
  
|Opción|¿Testigo?|Explicación|  
|------------|--------------|-----------------|  
|**Rendimiento alto (asincrónico)**|Null (si existe, no se usa excepto cuando la sesión requiere un quórum)|Para maximizar el rendimiento, la base de datos reflejada siempre estará algo detrás de la base de datos principal, nunca acercándose demasiado. Sin embargo, el espacio entre las bases de datos suele ser pequeño. La pérdida de un asociado tiene el siguiente efecto:<br /><br /> Si la instancia de servidor reflejado deja de estar disponible, el principal continúa.<br /><br /> Si la instancia del servidor principal deja de estar disponible, el servidor reflejado se detiene. Sin embargo, si la sesión no tiene testigos (recomendado) o el testigo se conecta al servidor reflejado, éste permanecerá inaccesible en estado de espera activa; el propietario de la base de datos puede forzar el servicio en la instancia del servidor reflejado (con una posible pérdida de datos).|  
|**Seguridad alta sin conmutación automática por error (sincrónico)**|No|Se garantiza que todas las transacciones confirmadas se escribirán en disco en el servidor reflejado.<br /><br /> La conmutación por error manual es posible cuando los asociados están conectados entre sí.<br /><br /> La pérdida de un asociado tiene el siguiente efecto:<br /><br /> Si la instancia de servidor reflejado deja de estar disponible, el principal continúa.<br /><br /> Si la instancia del servidor principal deja de estar disponible, el reflejo se detiene, pero está disponible como estado de espera activa; el propietario de la base de datos puede forzar el servicio en la instancia del servidor reflejado (con una posible pérdida de datos).|  
|**Seguridad alta con conmutación automática por error (sincrónico)**|Sí (obligatorio)|Máxima disponibilidad al incluir una instancia del servidor testigo para permitir la conmutación automática por error. Tenga en cuenta que solo puede seleccionar la opción **Seguridad alta con conmutación automática por error (sincrónico)** si antes ha especificado una dirección del servidor testigo.<br /><br /> La conmutación por error manual es posible cuando los asociados están conectados entre sí.<br /><br /> **\*\* Importante \*\*** Si el testigo se desconecta, los asociados deben estar conectados entre ellos para que la base de datos esté disponible. Para obtener más información, vea [Cuórum: cómo un testigo afecta a la disponibilidad de la base de datos &#40;creación de reflejo de la base de datos&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).<br /><br /> En los modos de funcionamiento sincrónicos, se garantiza que todas las transacciones confirmadas se escribirán en disco en el servidor reflejado. En la presencia de un testigo, la pérdida de un asociado tiene el siguiente efecto:<br /><br /> Si la instancia del servidor principal deja de estar disponible, se produce una conmutación automática por error. La instancia del servidor reflejado cambia al rol de servidor principal y ofrece su base de datos como base de datos principal.<br /><br /> Si la instancia de servidor reflejado deja de estar disponible, el principal continúa.<br /><br /> <br /><br /> Para más información, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).|  
  
 Una vez iniciada la creación de reflejo, puede cambiar el modo operativo y guardar el cambio haciendo clic en **Aceptar**.  
  
 Para obtener más información acerca de los modos de funcionamiento, vea [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **Estado**  
 Una vez que empieza la creación de reflejo, el panel **Estado** muestra el estado de la sesión de creación de reflejo de una base de datos desde que se ha seleccionado la página **Creación de reflejo**. Para actualizar el panel **Estado** , haga clic en el botón **Actualizar** . Los posibles estados son los siguientes:  
  
|Estados|Explicación|  
|------------|-----------------|  
|**Esta base de datos no se ha configurado para la creación de reflejo**|No existe ninguna sesión de creación de reflejo de la base de datos y no hay actividad de la que informar en la página **Creación de reflejo** .|  
|**En pausa**|La base de datos principal está disponible, pero no envía ningún registro al servidor reflejado.|  
|**Sin conexión**|La instancia del servidor principal no se puede conectar a su asociado.|  
|**Sincronizando**|El contenido de la base de datos reflejada va por detrás del contenido de la base de datos principal. La instancia de servidor principal envía las entradas de registro a la instancia del servidor reflejado, que aplica los cambios en la base de datos reflejada para confirmarla.<br /><br /> Al inicio de una sesión de creación de reflejo de la base de datos, las bases de datos reflejada y principal se encuentran en este estado.|  
|**Conmutación por error**|En la instancia de servidor principal se ha iniciado una conmutación por error manual (intercambio de roles); el servidor actualmente está pasando al rol reflejado. En este estado, las conexiones de los usuarios a la base de datos principal finalizan rápidamente. La base de datos adopta el rol reflejado poco después.|  
|**Sincronizado**|El estado de la base de datos cambia a **Sincronizado**cuando el servidor reflejado está suficientemente al día con respecto al servidor principal. La base de datos permanece en este estado mientras el servidor principal continúa con el envío de cambios al servidor reflejado, y el servidor reflejado continúa con la aplicación de los cambios en la base de datos reflejada.<br /><br /> En el modo de seguridad alta, es posible la conmutación por error sin pérdida de datos.<br /><br /> En el modo de rendimiento alto, siempre es posible que se pierdan datos, incluso en el estado **Sincronizado**.|  
  
 Para obtener más información, vea [Estados de creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).  
  
 **Actualizar**  
 Haga clic para actualizar el cuadro **Estado**.  
  
## Comentarios  
 Si no está familiarizado con la creación de reflejo de la base de datos, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
### Agregar un testigo a una sesión existente  
 Puede agregar un testigo a una sesión existente o reemplazar un testigo existente. Si conoce la dirección de red de servidor del testigo, puede escribirla en el campo **Testigo** manualmente. Si no la conoce, utilice el Asistente para la configuración de seguridad de la creación de reflejo de bases de datos para configurar el testigo. Después de que la dirección figure en el campo, asegúrese de que está seleccionada la opción **Seguridad alta con conmutación automática por error (sincrónico)**.  
  
 Tras configurar un nuevo testigo, debe hacer clic en **Aceptar** para agregarlo a la sesión de creación de reflejo.  
  
 **Para agregar un testigo al usar la Autenticación de Windows**  
  
 [Agregar o reemplazar un testigo de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### Quitar un testigo  
 Para quitar un testigo, elimine su dirección de red de servidor del campo **Testigo** . Si pasa del modo de alta seguridad con conmutación automática por error al modo de alto rendimiento, el campo **Testigo** se vacía de forma automática.  
  
 Después de eliminar el testigo, debe hacer clic en **Aceptar** para quitarlo de la sesión de creación de reflejo.  
  
### Supervisar la creación de reflejo de la base de datos  
 Para supervisar las bases de datos reflejadas en una instancia del servidor, puede usar el Monitor de creación de reflejo de la base de datos o el procedimiento almacenado del sistema sp_dbmmonitorresults.  
  
 **Para supervisar bases de datos reflejadas**  
  
-   [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 Para obtener más información, vea [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Especificar una dirección de red de servidor &#40;creación de reflejo de la base de datos&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md)  
  
-   [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## Vea también  
 [Seguridad de transporte para la creación de reflejo de la base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport security - database mirroring - always on availability.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Pausar y reanudar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [Quitar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [Testigo de creación de reflejo de la base de datos](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  