---
title: 'Lección 1: Conexión al motor de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 32b78c210647ab5b3722f01f334e9cb2e8bbfc13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63145492"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>Lección 1: Conexión al Motor de base de datos
  Al instalar [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], las herramientas instaladas dependen de la edición y de las opciones que seleccione al realizar la instalación. En esta lección se revisan las herramientas principales y se muestra cómo conectarse y realizar una función básica (autorizar a más usuarios).  
  
  
  
##  <a name="tools"></a> Herramientas de introducción  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] incluye varias herramientas. En este tema se describen las primeras herramientas que necesitará y se ofrece ayuda para seleccionar la herramienta adecuada para La tarea. Se puede obtener acceso a todas las herramientas desde el menú **Inicio** . No se instalan las mismas herramientas, como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], de forma predeterminada. Debe seleccionarlas como parte de los componentes de cliente durante la instalación. Para obtener una descripción completa de las herramientas descritas a continuación, búsquelas en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] solo contiene un subconjunto de las herramientas.  
  
### <a name="basic-tools"></a>Herramientas básicas  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] es la herramienta principal para administrar [!INCLUDE[ssDE](../includes/ssde-md.md)] y escribir código de [!INCLUDE[tsql](../includes/tsql-md.md)]. Se hospeda en el shell de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . No se incluye en [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] , pero está disponible como descarga independiente en el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?LinkId=144346).  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se instala con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las herramientas cliente. Permite habilitar protocolos de servidor, configurar opciones de protocolo, como los puertos TCP, configurar servicios de servidor para que se inicien automáticamente y configurar equipos cliente para que se conecten de la forma preferida. Esta herramienta configura los elementos de conectividad más avanzados, pero no habilita las características.  
  
### <a name="sample-database"></a>Base de datos de ejemplo  
 Las bases de datos de ejemplo y los ejemplos no están incluidos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La mayoría de los ejemplos descritos en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usan la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  
  
##### <a name="to-start-sql-server-management-studio"></a>Para iniciar SQL Server Management Studio  
  
-   En el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]y, a continuación, haga clic en **SQL Server Management Studio**.  
  
##### <a name="to-start-sql-server-configuration-manager"></a>Para iniciar el Administrador de configuración de SQL Server  
  
-   En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
##  <a name="connect"></a> Conectarse a Management Studio  
 Resulta sencillo conectarse a [!INCLUDE[ssDE](../includes/ssde-md.md)] desde herramientas que se ejecutan en el mismo equipo si conoce el nombre de la instancia y si se conecta como miembro del grupo Administradores del equipo. Los procedimientos siguientes deben realizarse en el mismo equipo en el que se hospeda [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>Para determinar el nombre de la instancia de motor de base de datos  
  
1.  Inicie una sesión en Windows como miembro del grupo Administradores y abra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
    > [!IMPORTANT]  
    >  Si se conecta a  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] en [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] o [!INCLUDE[nextref_longhorn](../includes/nextref-longhorn-md.md)] (o más reciente), es posible que tenga que hacer clic con el botón secundario en [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y luego hacer clic en **Ejecutar como administrador** para conectarse usando sus credenciales de administrador. A partir de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], el programa de instalación agrega inicios de sesión seleccionados a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], por lo que las credenciales de administrador no son necesarias.  
  
2.  En el cuadro de diálogo **Conectar con el servidor** , haga clic en **Cancelar**.  
  
3.  Si Servidores registrados no aparece, en el menú **Ver** , haga clic en **Servidores registrados**.  
  
4.  Con **Motor de base de datos** seleccionado en la barra de herramientas Servidores registrados, expanda **Motor de base de datos**, haga clic con el botón derecho en **Grupos de servidores locales**, seleccione **Tareas**y, después, haga clic en **Registrar servidores locales**. Se muestran todas las instancias de [!INCLUDE[ssDE](../includes/ssde-md.md)] instaladas en el equipo. La instancia predeterminada no tiene nombre y aparece como el nombre del equipo. Una instancia con nombre aparece como el nombre del equipo seguido de una barra inversa (\\) y del nombre de la instancia. En [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], la instancia se denomina *<nombre_equipo>* \sqlexpress, a no ser que se haya cambiado el nombre durante la instalación.  
  
##### <a name="to-verify-that-the-database-engine-is-running"></a>Para comprobar que el motor de base de datos está en ejecución  
  
1.  En Servidores registrados, si el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene un punto verde con una flecha blanca junto al nombre, [!INCLUDE[ssDE](../includes/ssde-md.md)] está en ejecución y no es necesario realizar ninguna otra acción.  
  
2.  Si el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene un punto rojo con un cuadrado blanco junto al nombre, [!INCLUDE[ssDE](../includes/ssde-md.md)] se encuentra detenido. Haga clic con el botón derecho en el nombre del [!INCLUDE[ssDE](../includes/ssde-md.md)], haga clic en **Control de servicios**y luego haga clic en **Iniciar**. Después de un cuadro de diálogo de confirmación, [!INCLUDE[ssDE](../includes/ssde-md.md)] debería iniciarse y el color del punto debería cambiar a verde con una flecha blanca.  
  
##### <a name="to-connect-to-the-database-engine"></a>Para conectarse al motor de base de datos  
  
1.  En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], en el menú **Archivo** , haga clic en **Conectar Explorador de objetos**.  
  
     Se abre el cuadro de diálogo **Conectar al servidor** . En el cuadro **Tipo de servidor** se muestra el último tipo de componente utilizado.  
  
2.  Seleccione **Motor de base de datos**.  
  
3.  En el cuadro **Nombre del servidor** , escriba el nombre de la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Para la instancia predeterminada de SQL Server, el nombre de servidor es el nombre del equipo. Para una instancia con nombre de SQL Server, el nombre del servidor es *<nombre_equipo>***\\***<nombre_instancia>,* como **ACCTG_SRVR\SQLEXPRESS**.  
  
4.  Haga clic en **Conectar**.  
  
##  <a name="additional"></a> Autorizar conexiones adicionales  
 Ahora que se ha conectado a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como administrador, una de las primeras tareas que debe realizar es autorizar a otros usuarios a conectarse. Para ello, cree un inicio de sesión y concédale autorización para obtener acceso a una base de datos como usuario. Los inicios de sesión pueden ser inicios de sesión con autenticación de Windows, que utilizan las credenciales de Windows, o bien inicios de sesión con autenticación de SQL Server, que almacenan la información de autenticación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y son independientes de las credenciales de Windows. Utilice la autenticación de Windows siempre que sea posible.  
  
##### <a name="create-a-windows-authentication-login"></a>Crear un inicio de sesión con autenticación de Windows  
  
1.  En la tarea anterior, se conectó a [!INCLUDE[ssDE](../includes/ssde-md.md)] utilizando [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. En el Explorador de objetos, expanda la instancia del servidor, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y, después, haga clic en **Nuevo inicio de sesión**.  
  
     Aparece el cuadro de diálogo **Inicio de sesión - Nuevo** .  
  
2.  En el **General** página, en el **nombre de inicio de sesión** , escriba un inicio de sesión de Windows en el formato  *\<dominio >\\< inicio de sesión\>* .  
  
3.  En el cuadro **Base de datos predeterminada** , seleccione [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , si está disponible. Si no lo está, seleccione **master**.  
  
4.  En la página **Roles del servidor** , si el nuevo inicio de sesión va a ser administrador, haga clic en **sysadmin**; de lo contrario, déjelo en blanco.  
  
5.  En la página **Asignación de usuarios** , seleccione **Asignar** para la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , si está disponible. Si no lo está, seleccione **master**. Observe que el cuadro **Usuario** se ha rellenado con el inicio de sesión. Al cerrar el cuadro de diálogo, se creará el usuario en la base de datos.  
  
6.  En el cuadro **Esquema predeterminado** , escriba **dbo** para asignar el inicio de sesión al esquema de propietario de base de datos.  
  
7.  Acepte los valores predeterminados de los cuadros **Elementos protegibles** y **Estado** y haga clic en **Aceptar** para crear el inicio de sesión.  
  
> [!IMPORTANT]  
>  Esta información es básica para empezar. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona un completo entorno de seguridad y, obviamente, la seguridad es un aspecto importante de las operaciones de base de datos.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Conexión desde otro equipo](lesson-2-connecting-from-another-computer.md)  
  
  
