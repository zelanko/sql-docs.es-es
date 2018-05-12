---
title: Configurar cuentas de servicio (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dff21ebf96bf957a7f390b8dea0010fa0396ff7d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="configure-service-accounts-analysis-services"></a>Configurar las cuentas de servicio (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El aprovisionamiento de cuentas para todo un producto se documenta en [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md), un tema que contiene gran cantidad de información sobre las cuentas de servicio de todos los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluido [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Consulte ese tema para obtener información sobre los tipos de cuenta válidos, los privilegios de Windows que se asignan durante la instalación, los permisos del sistema de archivos, los permisos del Registro, etc.  
  
 En este tema se ofrece información complementaria para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], que incluye los permisos adicionales necesarios para las instalaciones tabulares y para instalaciones en clúster. Además se ocupa de los permisos necesarios para admitir las operaciones del servidor. Por ejemplo, puede configurar operaciones de consultas y procesamiento para que se ejecuten en la cuenta del servicio, en cuyo caso deberá otorgar permisos adicionales para que funcione.  
  
-   [Privilegios de Windows asignados a Analysis Services](#bkmk_winpriv)  
  
-   [Permisos del sistema de archivos asignados a Analysis Services](#bkmk_FilePermissions)  
  
-   [Otorgar permisos adicionales para operaciones específicas del servidor](#bkmk_tasks)  
  
 Otro paso de configuración que aquí no se documenta es registrar un nombre de la entidad de seguridad (SPN) para la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y la cuenta de servicio. Con este paso, se habilita la autenticación de paso a través desde aplicaciones cliente a orígenes de datos back-end en escenarios de salto doble. Este paso solo se aplica a los servicios que se hayan configurado para delegación Kerberos restringida. Para obtener más instrucciones, vea [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) .  
  
## <a name="logon-account-recommendations"></a>Recomendaciones de la cuenta de inicio de sesión  
 En un clúster de conmutación por error, todas las instancias de Analysis Services deben configurarse para utilizar una cuenta de usuario con dominio de Windows. Asigne la misma cuenta a todas las instancias. Para obtener más detalles, consulte [Cómo agrupar en clúster Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) .  
  
 Instancias independientes deben usar la cuenta virtual predeterminada, **NT Service\MSSQLServerOLAPService** para la instancia predeterminada, o **servicio nt\msolap $ *** nombre de instancia* para una instancia con nombre. Esta recomendación se aplica a las instancias de Analysis Services en todos los modos de servidor, suponiendo que se dispone de un sistema operativo Windows Server 2008 R2 o posterior, y SQL Server 2012 o posterior para Analysis Services.  
  
## <a name="granting-permissions-to-analysis-services"></a>Otorgar permisos a Analysis Services  
 En esta sección se describen los permisos que Analysis Services requiere para las operaciones internas y locales, como iniciar el archivo ejecutable, leer el archivo de configuración y cargar bases de datos desde el directorio de datos. Si, en su lugar, busca orientación sobre cómo establecer permisos de acceso a datos externos e interoperabilidad con otros servicios y aplicaciones, consulte [Otorgar permisos adicionales para operaciones específicas del servidor](#bkmk_tasks) (más adelante en este tema).  
  
 Para las operaciones internas, el titular de los permisos de Analysis Services no es la cuenta de inicio de sesión, sino un grupo de seguridad de Windows creado por el programa de instalación y que contiene el SID por servicio. Asignar permisos al grupo de seguridad es un paso coherente con las versiones anteriores de Analysis Services. Además, las cuentas de inicio de sesión pueden cambiar con el tiempo, pero el SID por servicio y el grupo de seguridad local se mantienen constantes durante la vigencia de la instalación del servidor. En Analysis Services, esto hace que el grupo de seguridad sea una mejor opción para ser propietario de permisos, en lugar de la cuenta de inicio de sesión. Siempre que otorgue permisos manualmente a la instancia de servicio, ya se trate de permisos del sistema de archivos o de privilegios de Windows, asegúrese de que los otorga al grupo de seguridad local creado para la instancia del servidor.  
  
 El nombre del grupo de seguridad sigue un patrón. El prefijo es siempre **SQLServerMSASUser$**, le sigue el nombre del equipo y termina con el nombre de la instancia. La instancia predeterminada es **MSSQLSERVER**. Una instancia con nombre tendrá el nombre que se le haya dado durante la instalación.  
  
 Puede ver este grupo de seguridad en la configuración de seguridad local:  
  
-   Ejecute compmgmt.msc | **Usuarios y grupos locales** | **grupos** | **SQLServerMSASUser$**\<nombre del servidor >**$MSSQLSERVER**  (para una instancia predeterminada).  
  
-   Haga doble clic en el grupo de seguridad para ver sus miembros.  
  
 El único miembro del grupo es el SID por servicio. Junto a este se encuentra la cuenta de inicio de sesión. El nombre de la cuenta de inicio de sesión es estético: su función es dar contexto al SID por servicio. Si posteriormente cambia la cuenta de inicio de sesión y, a continuación, vuelve a esta página, observará que el grupo de seguridad y el SID por servicio no cambian, pero la etiqueta de la cuenta de inicio de sesión es diferente.  
  
##  <a name="bkmk_winpriv"></a> Privilegios de Windows asignados a la cuenta de servicio de Analysis Services  
 Analysis Services necesita permisos del sistema operativo para iniciar el servicio y para solicitar recursos del sistema. Los requisitos varían según el modo del servidor y en función de si la instancia está en clúster. Si no está familiarizado con los privilegios de Windows, vea los temas sobre [privilegios](http://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) y [constantes de privilegios (Windows)](http://msdn.microsoft.com/library/windows/desktop/bb530716\(v=vs.85\).aspx) para obtener más información.  
  
 Todas las instancias de Analysis Services requieren el privilegio **Iniciar sesión como servicio** (SeServiceLogonRight). El programa de instalación de SQL Server asigna automáticamente el privilegio en la cuenta de servicio que se haya especificado durante la instalación. Para los servidores que se ejecutan en el modo Multidimensional y Minería de datos, es el único privilegio de Windows que requiere la cuenta de servicio de Analysis Services para instalaciones de servidor aisladas y es el único privilegio que configura el programa de instalación para Analysis Services. Para instancias en clúster y tabulares, es preciso agregar manualmente privilegios de Windows.  
  
 Las instancias de clúster de conmutación por error, en el modo tabular o multidimensional, deben contar con **Aumentar prioridad de programación** (SeIncreaseBasePriorityPrivilege).  
  
 Las instancias tabulares usan los siguientes tres privilegios adicionales, que se deben otorgar de forma manual después de instalar la instancia.  
  
|||  
|-|-|  
|**Aumentar el espacio de trabajo de un proceso** (SeIncreaseWorkingSetPrivilege)|Este privilegio se encuentra disponible para todos los usuarios de forma predeterminada mediante el grupo de seguridad **Usuarios** . Si bloquea un servidor y, para ello, quita los privilegios de este grupo, es posible que Analysis Servicies no se inicie y se registre este error: "El cliente no dispone de un privilegio requerido". Cuando se produce este error, restablezca el privilegio para Analysis Services; para ello, otorgue el privilegio al grupo de seguridad de Analysis Services apropiado.|  
|**Ajustar las cuotas de la memoria para un proceso** (SeIncreaseQuotaSizePrivilege)|Este privilegio se usa para solicitar más memoria cuando un proceso dispone de recursos insuficientes para completar su ejecución, en función de los umbrales de memoria que se hubieran establecido para la instancia.|  
|**Bloquear páginas en la memoria** (SeLockMemoryPrivilege)|Este privilegio solo es necesario cuando la paginación está desactivada. De forma predeterminada, las instancias de servidor tabular usan el archivo de paginación de Windows, pero puede evitar que use la paginación de Windows si establece **VertiPaqPagingPolicy** en 0.<br /><br /> Si se establece**VertiPaqPagingPolicy** en 1 (predeterminado), la instancia del servidor tabular usará el archivo de paginación de Windows. Las asignaciones no están bloqueadas, de forma que Windows puede paginar según lo necesite. Como se está usando la paginación, no resulta necesario bloquear las páginas en la memoria. Por tanto, para la configuración predeterminada (donde **VertiPaqPagingPolicy** = 1), no es necesario conceder el privilegio **Bloquear páginas en memoria** a una instancia tabular.<br /><br /> **VertiPaqPagingPolicy** en 0. Si desactiva la paginación para Analysis Services, se bloquean las asignaciones, de forma que se asume que se ha otorgado el privilegio **Bloquear páginas en memoria** a la instancia tabular. Con esta configuración y el privilegio **Bloquear páginas en memoria** , Windows no puede paginar las asignaciones de memoria que se realicen para Analysis Services cuando el sistema se encuentre en condiciones de presión de memoria. Analysis Services confía en el permiso **Bloquear páginas en memoria** como exigencia para **VertiPaqPagingPolicy** = 0. Tenga en cuenta que no se recomienda desactivar la paginación de Windows. Se incrementaría el índice de errores por memoria insuficiente para las operaciones que de otra forma se realizarían correctamente si se hubiera permitido la paginación. Para más información acerca de [VertiPaqPagingPolicy](../../analysis-services/server-properties/memory-properties.md) , consulte **Memory Properties**.|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>Para ver o agregar privilegios de Windows en la cuenta de servicio  
  
1.  Ejecute GPEDIT.msc | Directiva de equipo local | Configuración del equipo | Configuración de Windows | Configuración de seguridad | Directivas locales | Asignaciones de derechos de usuario.  
  
2.  Revise las directivas existentes que incluyan **SQLServerMSASUser$**. Se trata de un grupo de seguridad local que se encuentra en los equipos con una instalación de Analysis Services. Tanto los privilegios de Windows como los permisos de las carpetas de archivos se otorgan a este grupo de seguridad. Haga doble clic en la directiva **Iniciar sesión como servicio** para ver cómo se ha especificado el grupo de seguridad en su sistema. El nombre completo del grupo de seguridad variará en función de si ha instalado Analysis Services como una instancia con nombre. Use este grupo de seguridad, en lugar de la propia cuenta de servicio, cuando vaya a agregar privilegios de cuenta.  
  
3.  Para agregar privilegios de cuenta en GPEDIT, haga clic con el botón derecho en **Aumentar el espacio de trabajo de un proceso** y seleccione **Propiedades**.  
  
4.  Haga clic en **Agregar grupo o usuario**.  
  
5.  Escriba el grupo de usuarios para la instancia de Analysis Services. Recuerde que la cuenta de servicio es un miembro de un grupo de seguridad local, lo cual requiere anteponer el nombre del equipo local al dominio de la cuenta.  
  
     En la lista siguiente se muestran dos ejemplos de una instancia predeterminada y una instancia con nombre denominada "Tabular" en una máquina denominada "SQL01-WIN12", donde el nombre de la máquina es el dominio local.  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  Repita el proceso para **Ajustar las cuotas de memoria de un proceso**y, opcionalmente, para **Bloquear páginas en memoria** o **Aumentar la prioridad de programación**.  
  
> [!NOTE]  
>  Las versiones anteriores del programa de instalación agregaban involuntariamente la cuenta de servicio de Analysis Services al grupo **Usuarios del registro de rendimiento** . Aunque este defecto se ha corregido, puede que las instalaciones existentes tengan esta pertenencia de grupo innecesaria. Puesto que no es necesario que la cuenta de servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pertenezca al grupo **Usuarios del registro de rendimiento** , puede quitarla del grupo.  
  
##  <a name="bkmk_FilePermissions"></a> Permisos del sistema de archivos asignados a la cuenta de servicio de Analysis Services  
  
> [!NOTE]  
>  Vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) para obtener una lista de permisos asociados a cada carpeta de programa.  
>   
>  Vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) para obtener información de permisos relacionada con la configuración de IIS y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Todos los permisos del sistema de archivos que se requieren para las operaciones de servidor, incluidos los permisos para cargar y descargar bases de datos de una carpeta de datos designada, los asigna el programa de instalación de SQL Server durante la instalación.  
  
 El titular de los permisos en los archivos de datos, ejecutables de archivos de programa, archivos de configuración, archivos de registro y archivos temporales es un grupo de seguridad local que crea el programa de instalación de SQL Server.  
  
 Por cada instancia que instale, se crea un grupo de seguridad. El grupo de seguridad se denomina la instancia: ya sea **SQLServerMSASUser$ MSSQLSERVER** para la instancia predeterminada, o **SQLServerMSASUser$**\<nombreDeServidor >$\< instancename > para una instancia con nombre. El programa de instalación aprovisiona este grupo de seguridad con los permisos de archivo necesarios para realizar operaciones de servidor. Si comprueba los permisos de seguridad del directorio \MSAS13.MSSQLSERVER\OLAP\BIN, verá que el grupo de seguridad (no la cuenta de servicio ni su SID por servicio) es el titular de los permisos de ese directorio.  
  
 El grupo de seguridad solo contiene un miembro: el identificador de seguridad (SID) por servicio de la cuenta de inicio de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El programa de instalación agrega un SID por servicio al grupo de seguridad local. El uso de un grupo de seguridad local, con su pertenencia de SID, constituye una diferencia pequeña pero apreciable de cómo el programa de instalación de SQL Server aprovisiona a Analysis Services, en comparación con el motor de base de datos.  
  
 Si cree que los permisos de archivo están dañados, siga estos pasos para comprobar que el servicio se sigue aprovisionando correctamente:  
  
1.  Use la herramienta de línea de comando de control de servicio (sc.exe) para obtener el SID de una instancia de servicio predeterminada.  
  
     `SC showsid MSSqlServerOlapService`  
  
     Para las instancias con nombre (en las que el nombre de la instancia sea Tabular), use esta sintaxis:  
  
     `SC showsid MSOlap$Tabular`  
  
2.  Use **Computer Manager** | **usuarios y grupos locales** | **grupos** para inspeccionar la pertenencia de SQLServerMSASUser$\<nombreDeServidor >$\<instancename > grupo de seguridad.  
  
     El miembro SID debería corresponderse con el SID por servicio del paso 1.  
  
3.  Use **Windows Explorer** | **Archivos de programa** | **Microsoft SQL Server** | MSASxx.MSSQLServer | **OLAP** | **ubicación** para comprobar que las propiedades de seguridad de carpeta se conceden al grupo de seguridad en el paso 2.  
  
> [!NOTE]  
>  Nunca quite o modifique un SID. Para restaurar un SID por servicio que se eliminó accidentalmente, vea [ http://support.microsoft.com/kb/2620201 ](http://support.microsoft.com/kb/2620201).  
  
 **Más información sobre SID por servicio**  
  
 Cada cuenta de Windows tiene un [SID](http://en.wikipedia.org/wiki/Security_Identifier)asociado, pero los servicios también pueden tener SID, por lo que nos referiremos a ellos como SID por servicio. Un SID por servicio se crea cuando se instala la instancia del servicio, como elemento único y permanente del servicio. El SID por servicio es un SID local de nivel de equipo que se genera a partir del nombre del servicio. En una instancia predeterminada, su nombre descriptivo es NT SERVICE\MSSQLServerOLAPService.  
  
 La ventaja de los SID por servicio es que permiten cambiar de manera arbitraria la cuenta de inicio de sesión más visible, sin que ello afecte a los permisos de archivos. Por ejemplo, suponga que ha instalado dos instancias de Analysis Services, una instancia predeterminada y una instancia con nombre, y que ambas se ejecutan en la misma cuenta de usuario de Windows. Si bien la cuenta de inicio de sesión es compartida, cada instancia de servicio contará con un SID por servicio único. Este SID es diferente al SID de la cuenta de inicio de sesión. El SID por servicio se usa para los permisos de archivos y los privilegios de Windows. En cambio, el SID de la cuenta de inicio de sesión se usa para escenarios de autenticación y autorización (se usan SID diferentes para cada propósito).  
  
 Dado que el SID es inmutable, las ACL del sistema de archivos se crean durante la instalación del servicio y se pueden usar de forma indefinida, independientemente de la frecuencia con la que se cambie la cuenta de servicio. Como medida de seguridad adicional, las ACL que especifican permisos mediante un SID aseguran que solo una única instancia de un servicio tiene acceso a los archivos ejecutables de programas y a las carpetas de datos, incluso aunque haya otros servicios que se ejecuten bajo la misma cuenta.  
  
##  <a name="bkmk_tasks"></a> Otorgar permisos adicionales de Analysis Servicies para operaciones de servidor específicas  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ejecuta algunas tareas en el contexto de seguridad de la cuenta de servicio (o la cuenta de inicio de sesión) que se usa para iniciar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y ejecuta otras tareas en el contexto de seguridad del usuario que solicita la tarea.  
  
 En la tabla siguiente se describen los permisos adicionales necesarios para que las tareas se ejecuten como la cuenta de servicio.  
  
|Operación del servidor|Elemento de trabajo|Justificación|  
|----------------------|---------------|-------------------|  
|Acceso remoto a orígenes de datos relacionales externos|Crear un inicio de base de datos para la cuenta de servicio|El procesamiento se refiere a la recuperación de datos de un origen de datos externo (normalmente una base de datos relacional), que después se carga en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Una de las opciones de credenciales para recuperar datos externos consiste en usar la cuenta de servicio. Esta opción de credenciales solo funciona si crea un inicio de sesión de la base de datos para la cuenta de servicio y concede permisos de lectura para la base de datos de origen. Vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md) para obtener más información sobre cómo usar la opción de cuenta de servicio para esta tarea. Del mismo modo, si se emplea el modo de almacenamiento ROLAP, están disponibles las mismas opciones de suplantación. En este caso, la cuenta debe disponer también de acceso de escritura a los datos de origen para procesar las particiones ROLAP (es decir, para almacenar agregaciones).|  
|DirectQuery|Crear un inicio de base de datos para la cuenta de servicio|DirectQuery es una característica tabular que se usa para consultar conjuntos de datos externos que son demasiado grandes y no caben en el modelo tabular o que tienen otras características que hacen que sea mejor usar DirectQuery que la opción predeterminada de almacenamiento en memoria. Una de las opciones de conexión disponibles en el modo DirectQuery es usar la cuenta de servicio. De nuevo, esta opción solo funciona cuando la cuenta de servicio tiene un inicio de sesión de la base de datos y permisos de lectura en el origen de datos de destino. Vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md) para obtener más información sobre cómo usar la opción de cuenta de servicio para esta tarea. También se pueden usar las credenciales del usuario actual para recuperar datos. En la mayoría de los casos, esta opción conlleva una conexión de doble salto, por lo que debe asegurarse de configurar la cuenta de servicio para la delegación limitada de Kerberos de forma que la cuenta de servicio pueda delegar las identidades en un servidor que sigue en la cadena. Para obtener más información, vea [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).|  
|Acceso remoto a otras instancias de SSAS|Agregar la cuenta de servicio a los roles de base de datos de Analysis Services que se definieron en el servidor remoto|Las particiones remotas y la referencia a objetos vinculados en otras instancias remotas de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son capacidades del sistema que requieren permisos en un equipo o dispositivo remoto. Cuando una persona crea y rellena particiones remotas, o cuando configura un objeto vinculado, esa operación se ejecuta en el contexto de seguridad del usuario actual. Si más adelante automatiza estas operaciones, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tendrá acceso a las instancias remotas en el contexto de seguridad de su cuenta de servicio. Para obtener acceso a objetos vinculados en una instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la cuenta de inicio de sesión debe tener permiso para leer los objetos adecuados en la instancia remota como, por ejemplo, permiso de acceso de lectura a determinadas dimensiones. Del mismo modo, el uso de particiones remotas requiere que la cuenta de servicio tenga derechos administrativos en la instancia remota. Esos permisos se conceden en la instancia remota de Analysis Services, mediante roles que asocian las operaciones permitidas a un objeto concreto. Vea [Otorgar permisos de base de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obtener instrucciones sobre cómo conceder permisos de Control total que permitan operaciones de procesado y consulta. Consulte [Crear y administrar una partición remota &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md) para obtener más información sobre las particiones remotas.|  
|Reescritura|Agregar la cuenta de servicio a los roles de base de datos de Analysis Services que se definieron en el servidor remoto|Cuando se habilita en aplicaciones cliente, la reescritura es una característica de los modelos multidimensionales que permite la creación de nuevos valores de datos durante el análisis de datos. Si la reescritura está habilitada en cualquier dimensión o cubo, la cuenta de servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe disponer de permisos de escritura sobre la tabla de reescritura de la base de datos relacional de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si esta tabla todavía no existe y es necesario crearla, la cuenta de servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe disponer también de permisos para crear la tabla dentro de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] designada.|  
|Escribir en una tabla del registro de consultas de una base de datos relacional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Crear un inicio de base de datos para la cuenta de servicio y asignar permisos de escritura en la tabla del registro de consultas|Puede habilitar el registro de consultas para recopilar datos de uso de una tabla de la base de datos para su análisis posterior. La cuenta de servicio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] debe disponer de permisos de escritura sobre la tabla del registro de consultas de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] designada. Si esta tabla todavía no existe y es necesario crearla, la cuenta de inicio de sesión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deberá disponer también de permisos para crear la tabla en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] designada. Para obtener más información, vea las entradas de blog [Improve SQL Server Analysis Services Performance with the Usage Based Optimization Wizard](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) (Mejorar el rendimiento de SQL Server Analysis Services con el Asistente para optimización basada en el uso) y [Query Logging in Analysis Services](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx)(Registro de consultas de Analysis Services).|  
  
## <a name="see-also"></a>Vea también  
 [Configurar los permisos y cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Cuenta de servicio de SQL Server y SID por servicio (Blog)](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [SQL Server usa un SID de servicio para proporcionar aislamiento del servicio (artículo de KB)](http://support.microsoft.com/kb/2620201)   
 [Token de acceso (MSDN)](http://msdn.microsoft.com/library/windows/desktop/aa374909\(v=vs.85\).aspx)   
 [Identificadores de seguridad (MSDN)](http://msdn.microsoft.com/library/windows/desktop/aa379571\(v=vs.85\).aspx)   
 [Token de acceso (Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [Listas de control de acceso (Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
