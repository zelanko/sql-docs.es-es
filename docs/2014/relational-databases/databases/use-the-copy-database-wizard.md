---
title: Usar el Asistente para copiar bases de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.cdw.transfermethod.f1
- sql12.swb.cdw.welcome.f1
- sql12.swb.cdw.packageconfiguration.f1
- sql12.swb.cdw.schedule.f1
- sql12.swb.cdw.destination.f1
- sql12.swb.cdw.complete.f1
- sql12.swb.cdw.destinationconfiguration.f1
- sql12.swb.cdw.selectdatabaseobjects.f1
- sql12.swb.cdw.databases.f1
- sql12.swb.cdw.source.f1
- sql12.swb.cdw.locationofsourcedbfiles.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e72b960db0fd5b733119cafeca98f124eaa15f38
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871142"
---
# <a name="use-the-copy-database-wizard"></a>Usar el Asistente para copiar bases de datos
  El Asistente para copiar bases de datos permite mover o copiar bases de datos y sus objetos de un servidor a otro fácilmente, sin tiempo de inactividad del servidor. También puede actualizar las bases de datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Mediante este asistente, puede hacer lo siguiente:  
  
-   Elegir un servidor de origen y de destino  
  
-   Seleccionar las bases de datos que se van a mover, copiar o actualizar.  
  
-   Especificar la ubicación del archivo de las bases de datos.  
  
-   Crear inicios de sesión en el servidor de destino.  
  
-   Copiar otros objetos de ayuda, trabajos, mensajes de error y procedimientos almacenados definidos por el usuario.  
  
-   Programar cuándo mover o copiar las bases de datos.  
  
 Además de copiar las bases de datos, puede copiar los metadatos asociados, como los inicios de sesión y los objetos de la base de datos **maestra** necesarios para una base de datos copiada.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Uso del Asistente para copiar bases de datos para:**  
  
     [Copiar, trasladar o actualizar bases de datos](#Copy_Move)  
  
-   **Seguimiento después de la actualización:**  
  
     [Después de actualizar una base de datos de SQL Server](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Asistente para copiar bases de datos no está disponible en la edición Express.  
  
-   El Asistente para copiar bases de datos no se puede usar para copiar o mover las bases de datos siguientes.  
  
    -   Bases de datos del sistema  
  
    -   Bases de datos marcadas para la replicación.  
  
    -   Las bases de datos marcadas como no accesibles, en carga, sin conexión, en recuperación, sospechosas o en modo de emergencia.  
  
-   Una vez actualizada la base de datos, no se puede degradar a una versión anterior.  
  
-   Si selecciona la opción **Mover** , el asistente elimina automáticamente la base de datos de origen después de moverla. El Asistente para copiar bases de datos no elimina una base de datos de origen si se selecciona la opción **Copiar** .  
  
-   Si usa el método de objeto de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para mover el catálogo de texto completo, debe volver a rellenar el índice después del movimiento.  
  
-   El método de separar y adjuntar separa la base de datos, mueve o copia los archivos .mdf, .ndf y .ldf de la base de datos y vuelve a adjuntar la base de datos en la nueva ubicación. En el método de separar y adjuntar, para evitar la incoherencia o la pérdida de datos, las sesiones activas no pueden adjuntarse a la base de datos que se van a copiar o mover. Si existe alguna sesión activa, el Asistente para copiar bases de datos no ejecuta la operación de mover o copiar. En el método de objeto de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se permiten las sesiones activas porque la base de datos nunca está sin conexión.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Asegúrese de que el Agente SQL Server se inició en el servidor de destino.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
  
-   Para asegurarse del rendimiento óptimo de una base de datos actualizada, ejecute sp_updatestats (actualizar estadísticas) en la base de datos actualizada.  
  
-   Al copiar una base de datos a otra instancia de servidor, para que los usuarios y las aplicaciones puedan utilizarla de igual manera, puede que tenga que volver a crear algunos o todos los metadatos de la base de datos, como los inicios de sesión y los trabajos, en la otra instancia de servidor. Para obtener más información, vea [administrar los metadatos cuando una base de datos está disponible en otra instancia de servidor &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Debe ser miembro del rol fijo de servidor **sysadmin** tanto en el servidor de origen como en el servidor de destino.  
  
##  <a name="copy-move-or-upgrade-databases"></a><a name="Copy_Move"></a>Copiar, trasladar o actualizar bases de datos  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Bases de datos**, haga clic con el botón secundario en una base de datos, seleccione **Tareas**y, a continuación, haga clic en **Copiar base de datos**.  
  
2.  En la página **Seleccionar un servidor de origen** , especifique el servidor donde se encuentra la base de datos que se va a mover o copiar, y para escribir la información de inicio de sesión. Después de seleccionar el método de autenticación y especificar la información de inicio de sesión, haga clic en **Siguiente** para establecer la conexión al servidor de origen. Esta conexión permanece abierta durante toda la sesión.  
  
     **Servidor de origen**  
     Seleccione el nombre del servidor donde se encuentra la base de datos o las bases de datos que desea mover o copiar, o haga clic en el botón examinar (**...**) para buscar el servidor que desee. El servidor debe ser por lo menos [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
     **Usar autenticación de Windows**  
     Permita que un usuario se conecte a través de una cuenta de usuario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Usar autenticación SQL Server**  
     Permita que un usuario se conecte mediante un nombre de usuario y una contraseña de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Nombre de usuario**  
     Escriba el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
     **Contraseña**  
     Escriba la contraseña del inicio de sesión. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
     **Siguiente**  
     Conéctese al servidor y valide el usuario. Este proceso comprueba si el usuario es miembro del rol fijo de servidor **sysadmin** en el equipo seleccionado.  
  
3.  En la página **Seleccionar un servidor de destino** , especifique el servidor al que se va a mover o copiar la base de datos. Si establece los servidores de origen y de destino en la misma instancia de servidor, realizará una copia de una base de datos. En este caso, debe cambiar el nombre de la base de datos posteriormente en el asistente. Puede usarse el nombre de la base de datos de origen para la base de datos copiada o movida únicamente si no existe algún conflicto de nombres en el servidor de destino. Si existe algún conflicto de nombre, debe solucionarse manualmente en el servidor de destino antes de poder utilizar el nombre de la base de datos de origen.  
  
     **Servidor de destino**  
     Seleccione el nombre del servidor al que va a moverse o copiarse la base de datos o las bases de datos, o haga clic en el botón Examinar (**...**) para buscar un servidor de destino.  
  
    > [!NOTE]  
    >  Puede usar un destino que sea un servidor en clúster; el Asistente para copiar bases de datos se asegurará de que solo se seleccionen unidades compartidas en un servidor de destino en clúster.  
  
     **Usar autenticación de Windows**  
     Permita que un usuario se conecte a través de una cuenta de usuario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Usar autenticación SQL Server**  
     Permita que un usuario se conecte mediante un nombre de usuario y una contraseña de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Nombre de usuario**  
     Escriba el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Contraseña**  
     Escriba la contraseña del inicio de sesión. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     **Siguiente**  
     Conéctese al servidor y valide el usuario. Este proceso comprueba si el usuario tiene los permisos enumerados anteriormente en los equipos seleccionados.  
  
4.  En la página **Seleccionar el método de transferencia** , seleccione el método de transferencia.  
  
     **Usar el método de separar y adjuntar**  
     Esta opción separa la base de datos del servidor de origen, copia los archivos de base de datos (.mdf, .ndf y .ldf) al servidor de destino y adjunta la base de datos al servidor de destino. Generalmente, este método es el más rápido, ya que la tarea principal consiste en leer el disco de origen y escribir en el disco de destino. No se necesita lógica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para crear objetos en la base de datos ni para crear estructuras de almacenamiento de datos. Sin embargo, este método puede ser más lento si la base de datos contiene una gran cantidad de espacio asignado, pero sin utilizar. Por ejemplo, una nueva base de datos casi vacía que se crea con una asignación de 100 MB, copia los 100 MB, aunque solo se utilicen 5 MB.  
  
    > [!NOTE]  
    >  Este método impide que la base de datos esté disponible para los usuarios durante la transferencia.  
  
     **Si se produce un error, volver a adjuntar la base de datos de origen**  
     Cuando se copia una base de datos, los archivos originales de la base de datos siempre se vuelven a adjuntar al servidor de origen. Utilice este cuadro para volver a adjuntar los archivos originales a la base de datos de origen si no se puede mover una base de datos.  
  
     **Usar el método de objeto de administración de SQL**  
     Este método lee la definición de cada objeto de la base de datos de origen y lo crea en la base de datos de destino. A continuación, transfiere los datos de las tablas de origen a las tablas de destino y vuelve a crear los índices y metadatos.  
  
    > [!NOTE]  
    >  Los usuarios de la base de datos pueden tener acceso a ella durante la transferencia.  
  
5.  En la página **Seleccionar base de datos** , seleccionar la base de datos o las bases de datos que desea mover o copiar del servidor de origen al servidor de destino. Vea [limitaciones y restricciones](#Restrictions) en la sección ' antes de empezar ' de este tema.  
  
     **Move**  
     Seleccione esta opción para mover la base de datos al servidor de destino.  
  
     **Copiar**  
     Seleccione esta opción para copiar la base de datos al servidor de destino.  
  
     **Origen**  
     Muestra las bases de datos que hay en el servidor de origen.  
  
     **Estado**  
     Muestra **Aceptar** si la base de datos se puede mover. En caso contrario, muestra el motivo por el que la base de datos no se puede mover.  
  
     **Actualizar**  
     Actualiza la lista de bases de datos.  
  
     **Siguiente**  
     Inicia el proceso de validación y pasa a la pantalla siguiente.  
  
6.  En la página **Configurar base de datos de destino** , cambie el nombre de la base de datos si es adecuado y especifique la ubicación y los nombres de los archivos de base de datos. Esta página aparecerá una vez para cada base de datos que se mueva o se copie.  
  
7.  En la página **Seleccionar objetos de base de datos** , seleccione los objetos que desee incluir en la operación de mover o copiar. Esta página solo está disponible cuando el origen y el destino están en servidores diferentes. Para incluir un objeto, haga clic en el nombre del objeto en el cuadro **Objetos relacionados disponibles** y, después, haga clic en el botón **>>** para mover el objeto al cuadro **Objetos relacionados seleccionados** . Para excluir un objeto, haga clic en el nombre del objeto en el cuadro **objetos relacionados seleccionados** y ** < ** , a continuación, haga clic en el botón para desplace el objeto al cuadro **objetos relacionados disponibles** . De forma predeterminada, se transfieren todos los objetos de cada tipo seleccionado. Para elegir objetos individuales de cualquier tipo, haga clic en el botón de puntos suspensivos situado junto a cualquier tipo de objeto en el cuadro **Objetos relacionados seleccionados** . Se abrirá un cuadro de diálogo en el que podrá seleccionar objetos individuales.  
  
     **Inicios de sesión (todos los inicios de sesión en tiempo de ejecución)**  
     Incluye los inicios de sesión en la operación de mover o copiar. La opción está seleccionada de forma predeterminada.  
  
     **Procedimientos almacenados de la base de datos maestra**  
     Incluye los procedimientos almacenados de la base de datos **maestra** en la operación de mover o copiar.  
  
    > [!NOTE]  
    >  No se pueden elegir procedimientos almacenados extendidos y sus DLL asociadas para realizar copias automáticas.  
  
     **trabajos del Agente SQL Server**  
     Incluye los trabajos de la base de datos **msdb** en la operación de mover o copiar.  
  
     **Mensajes de error definidos por el usuario**  
     Incluye los mensajes de error definidos por el usuario en la operación de mover o copiar.  
  
     **Puntos de conexión**  
     Incluye los extremos definidos en la base de datos de origen.  
  
     **Catálogo de texto completo**  
     Incluye los catálogos de texto completo de la base de datos de origen.  
  
     **Paquete SSIS**  
     Incluye los paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] definidos en la base de datos de origen.  
  
     **Descripción**  
     Descripción del objeto.  
  
8.  En la página **Ubicación de los archivos de base de datos de origen** , especifique un recurso compartido del sistema de archivos que contenga los archivos de base de datos del servidor de origen. Es obligatorio si las instancias de servidor de origen y destino están en equipos diferentes.  
  
     **Base de datos**  
     Muestra el nombre de las bases de datos que se mueven.  
  
     **Ubicación de la carpeta**  
     Especifique la ubicación de los archivos de la base de datos de origen en el sistema de archivos.  
  
     Por ejemplo: C:\Archivos de programa\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA  
  
     **Recurso compartido de archivos en el servidor de origen**  
     Especifique la ubicación de los archivos de la base de datos de origen como una ruta de un recurso compartido de archivos.  
  
     Por ejemplo: "\\\\*SERVER_NAME*\c $ \Archivos de programa\Microsoft SQL Server\MSSQL110. MSSQLSERVER\MSSQL\Data  
  
9. El Asistente para copiar bases de datos crea un paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] para transferir la base de datos de la página **Configurar el paquete** y personalizar el paquete si procede.  
  
     **Ubicación del paquete**  
     Muestra el lugar donde se escribirá el paquete [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
     **Nombre del paquete**  
     Especifique un nombre para el paquete de [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
     **Opciones de registro**  
     Seleccione si desea almacenar la información de registro en un archivo de texto o en el registro de eventos de Windows.  
  
     **Ruta del archivo de registro de errores**  
     Proporcione una ruta de acceso para la ubicación del archivo de registro. Esta opción solo está disponible si está seleccionada la opción de registro del archivo de texto.  
  
10. En la página **Programar el paquete** , especifique cuándo desea que se inicie la operación de mover o copiar. Si no es administrador del sistema, debe especificar una cuenta de proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con acceso al subsistema de ejecución de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS).  
  
     **Ejecutar inmediatamente**  
     Inicia la operación de mover o copiar después de hacer clic en **Siguiente**.  
  
     **Programación**  
     Inicia la operación de mover o copiar más adelante. La configuración del programa actual aparece en el cuadro de descripción. Para cambiar la programación, haga clic en **Cambiar**.  
  
     **Cambios**  
     Abre el cuadro de diálogo **Nueva programación de trabajo** .  
  
     **Cuenta de proxy de Integration Services**  
     Seleccione una cuenta de proxy disponible. Para programar la transferencia, el usuario debe disponer al menos de una cuenta de proxy, configurada con permisos para el **Subsistema de ejecución de paquetes SSIS** .  
  
     Para crear una cuenta para la ejecución de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , en el Explorador de objetos, expanda **Agente SQL Server**, expanda **Servidores proxy**, haga clic con el botón secundario en **Ejecución de paquete SSIS**y, a continuación, haga clic en **Nuevo proxy**.  
  
     Los miembros del rol fijo de servidor **sysadmin** pueden seleccionar la **Cuenta del servicio del Agente SQL Server**, que tiene todos los permisos necesarios.  
  
11. En la página **Finalización del asistente** , revise el resumen de las opciones seleccionadas. Haga clic en **Atrás** para cambiar una opción. Haga clic en **Finalizar** para crear la base de datos. Durante la transferencia, la página **Realizando operación** supervisa la información de estado acerca de la ejecución del **Asistente para copiar bases de datos**.  
  
     **Acción**  
     Enumera cada acción que se está ejecutando.  
  
     **Estado**  
     Indica si la acción, en su conjunto, concluyó correctamente o no.  
  
     **Mensaje**  
     Proporciona los mensajes devueltos en cada paso.  
  
##  <a name="follow-up-after-upgrading-a-sql-server-database"></a><a name="FollowUp"></a> Seguimiento: Después de actualizar una base de datos de SQL Server  
 Después de usar el Asistente para actualizar una base de datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos está disponible inmediatamente y se actualiza de forma automática. Si la base de datos tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, en función del valor de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la importación puede requerir varias horas y volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que cuando la opción de actualización se establece en **importar**, si un catálogo de texto completo no está disponible, se vuelven a generar los índices de texto completo asociados. Para obtener más información sobre cómo ver o cambiar la configuración de la propiedad **Opción de actualización de texto completo** , vea [Administrar y supervisar la búsqueda de texto completo para una instancia de servidor](../search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 Si el nivel de compatibilidad de una base de datos de usuario era 100 o superior antes de la actualización, permanece igual después de la misma. Si el nivel de compatibilidad era 90 en la base de datos actualizada, el nivel de compatibilidad se establece en 100, que es el nivel de compatibilidad mínimo admitido en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar una base de datos mediante separar y adjuntar &#40;Transact-SQL&#41;](upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [Create a SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  
