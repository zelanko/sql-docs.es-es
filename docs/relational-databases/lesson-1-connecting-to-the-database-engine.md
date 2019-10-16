---
title: 'Lección 1: Conexión al motor de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 02/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: quickstart
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1ab78eab73526568736dea8c4aef1525b2607c93
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2019
ms.locfileid: "72162558"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>Lección 1: Conexión al Motor de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Al instalar [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], las herramientas instaladas dependen de la edición y de las opciones que seleccione al realizar la instalación. En esta lección se revisan las herramientas principales y se muestra cómo conectarse y realizar una función básica (autorizar a más usuarios).  

Esta lección contiene las siguientes tareas:  
- [Herramientas de introducción](#tools)  
- [Conectarse a Management Studio](#connect)  
- [Autorizar conexiones adicionales](#additional) 

## <a name="tools">Herramientas de introducción</a> 
- [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] incluye varias herramientas. En este tema se describen las primeras herramientas que necesitará y se ofrece ayuda para seleccionar la herramienta adecuada para La tarea. Se puede obtener acceso a todas las herramientas desde el menú **Inicio** . No se instalan las mismas herramientas, como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], de forma predeterminada. Debe seleccionarlas como parte de los componentes de cliente durante la instalación. Para obtener una descripción completa de las herramientas descritas a continuación, búsquelas en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] solo contiene un subconjunto de las herramientas.  

### <a name="basic-tools"></a>Herramientas básicas
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) es la herramienta principal para administrar el [!INCLUDE[ssDE](../includes/ssde-md.md)] y escribir código de [!INCLUDE[tsql](../includes/tsql-md.md)] . Se hospeda en el shell de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . SSMS está disponible para su descarga gratuita en el [Centro de descarga de Microsoft](https://msdn.microsoft.com/library/mt238290.aspx). La última versión puede usarse con versiones anteriores del [!INCLUDE[ssDE_md](../includes/ssde-md.md)].  

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se instala con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las herramientas cliente. Permite habilitar protocolos de servidor, configurar opciones de protocolo, como los puertos TCP, configurar servicios de servidor para que se inicien automáticamente y configurar equipos cliente para que se conecten de la forma preferida. Esta herramienta configura los elementos de conectividad más avanzados, pero no habilita las características.  

### <a name="sample-database"></a>Base de datos de ejemplo
Las bases de datos de ejemplo y los ejemplos no están incluidos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La mayoría de los ejemplos descritos en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usan la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  

##### <a name="to-start-sql-server-management-studio"></a>Para iniciar SQL Server Management Studio
- En las versiones actuales de Windows, en la página de **inicio** , escriba SSMS y, después, haga clic en **Microsoft SQL Server Management Studio**.  
- Si usa versiones anteriores de Windows, en el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]y luego haga clic en **SQL Server Management Studio**.  

##### <a name="to-start-sql-server-configuration-manager"></a>Para iniciar el Administrador de configuración de SQL Server  
- En las versiones actuales de Windows, en la página de **Inicio** , escriba **Administrador de configuración**y luego haga clic en **Administrador de configuración de SQL Server *versión* Administrador de configuración**.   
- Si usa versiones anteriores de Windows, en el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **Herramientas de configuración**y, después, haga clic en **Administrador de configuración de SQL Server**.  

## <a name="connect"></a>Conectarse a Management Studio  
- Resulta sencillo conectarse a [!INCLUDE[ssDE](../includes/ssde-md.md)] desde herramientas que se ejecutan en el mismo equipo si conoce el nombre de la instancia y se conecta como miembro del grupo local Administradores del equipo. Los procedimientos siguientes deben realizarse en el mismo equipo en el que se hospeda [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

> [!NOTE]  
> En este tema se trata la conexión a un SQL Server local. Para conectarse a Azure SQL Database, consulte [Conexión a SQL Database con SQL Server Management Studio y ejecución de una consulta T-SQL de ejemplo](https://azure.microsoft.com/documentation/articles/sql-database-connect-query-ssms/).  

##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>Para determinar el nombre de la instancia de motor de base de datos  

1.  Inicie una sesión en Windows como miembro del grupo Administradores y abra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
2.  En el cuadro de diálogo **Conectar con el servidor** , haga clic en **Cancelar**.  
3.  Si Servidores registrados no aparece, en el menú **Ver** , haga clic en **Servidores registrados**.
4.  Con **Motor de base de datos** seleccionado en la barra de herramientas Servidores registrados, expanda **Motor de base de datos**, haga clic con el botón derecho en **Grupos de servidores locales**, seleccione **Tareas**y, después, haga clic en **Registrar servidores locales**. Expanda **Grupos de servidores locales** para ver todas las instancias del [!INCLUDE[ssDE](../includes/ssde-md.md)] instalado en el equipo mostrado. La instancia predeterminada no tiene nombre y aparece como el nombre del equipo. Una instancia con nombre aparece como el nombre del equipo seguido de una barra inversa (\\) y del nombre de la instancia. En [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], la instancia se denomina *<nombre_equipo>* \sqlexpress, a no ser que se haya cambiado el nombre durante la instalación.  

[!INCLUDE[fresh-note-steps-feedback](../includes/paragraph-content/fresh-note-steps-feedback.md)]

##### <a name="to-verify-that-the-database-engine-is-running"></a>Para comprobar que el motor de base de datos está en ejecución

1.  En Servidores registrados, si el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene un punto verde con una flecha blanca junto al nombre, [!INCLUDE[ssDE](../includes/ssde-md.md)] está en ejecución y no es necesario realizar ninguna otra acción.  

2.  Si el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene un punto rojo con un cuadrado blanco junto al nombre, [!INCLUDE[ssDE](../includes/ssde-md.md)] se encuentra detenido. Haga clic con el botón derecho en el nombre del [!INCLUDE[ssDE](../includes/ssde-md.md)], haga clic en **Control de servicios**y luego haga clic en **Iniciar**. Después de un cuadro de diálogo de confirmación, [!INCLUDE[ssDE](../includes/ssde-md.md)] debería iniciarse y el color del punto debería cambiar a verde con una flecha blanca.  

##### <a name="to-connect-to-the-database-engine"></a>Para conectarse al motor de base de datos  

Se ha seleccionado al menos una cuenta de administrador al instalar [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] . Realice el siguiente paso con la sesión iniciada en Windows como administrador.

1.  En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], en el menú **Archivo** , haga clic en **Conectar Explorador de objetos**. 
- Se abre el cuadro de diálogo **Conectar al servidor** . En el cuadro **Tipo de servidor** se muestra el último tipo de componente utilizado.  

2.  Seleccione **Motor de base de datos**.

![object-explorer](../relational-databases/media/object-explorer.png)

3.  En el cuadro **Nombre del servidor** , escriba el nombre de la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Para la instancia predeterminada de SQL Server, el nombre de servidor es el nombre del equipo. Para una instancia con nombre de SQL Server, el nombre del servidor es _\<nombre_equipo\>_ **\\** _\<nombre_instancia\>_ , como **ACCTG_SRVR\SQLEXPRESS**. En la siguiente captura de pantalla se muestra la conexión a la instancia predeterminada (sin nombre) de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] en un equipo denominado "PracticeComputer". El usuario que ha iniciado sesión en Windows es Mary del dominio Contoso. Al usar la autenticación de Windows, no puede cambiar el nombre de usuario. 

![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  Haga clic en **Conectar**.

> [!NOTE]
> En este tutorial se supone que es nuevo con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y no tiene problemas especiales para conectarse. Esto debería ser suficiente para la mayoría de las personas y hace que este tutorial sea simple. Para obtener pasos de solución de problemas detallados, consulte [Solucionar problemas de conexión al motor de base de datos de SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md). 

## <a name="additional"></a>Autorizar conexiones adicionales  
Ahora que se ha conectado a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como administrador, una de las primeras tareas que debe realizar es autorizar a otros usuarios a conectarse. Para ello, cree un inicio de sesión y concédale autorización para obtener acceso a una base de datos como usuario. Los inicios de sesión pueden ser inicios de sesión con autenticación de Windows, que utilizan las credenciales de Windows, o bien inicios de sesión con autenticación de SQL Server, que almacenan la información de autenticación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y son independientes de las credenciales de Windows. Utilice la autenticación de Windows siempre que sea posible.

> [!TIP]
> La mayoría de las organizaciones tienen usuarios del dominio y usarán la autenticación de Windows. Puede probar usted mismo mediante la creación de usuarios locales adicionales en el equipo. El equipo autenticará los usuarios locales, por lo que el dominio es el nombre del equipo. Por ejemplo, si el equipo se denomina `MyComputer` y crea un usuario denominado `Test`, la descripción de Windows del usuario es `Mycomputer\Test`.  

##### <a name="create-a-windows-authentication-login"></a>Crear un inicio de sesión con autenticación de Windows 

1.  En la tarea anterior, se conectó a [!INCLUDE[ssDE](../includes/ssde-md.md)] utilizando [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. En el Explorador de objetos, expanda la instancia del servidor, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y, después, haga clic en **Nuevo inicio de sesión**. Aparece el cuadro de diálogo **Inicio de sesión - Nuevo** .  

2.  En la página **General** , en el cuadro **Nombre de inicio de sesión** , escriba un inicio de sesión de Windows con el formato: `<domain>\\<login>`

![new-login](../relational-databases/media/new-login.png)

3.  En el cuadro **Base de datos predeterminada** , seleccione [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , si está disponible. Si no lo está, seleccione **master**.  
4.  En la página **Roles del servidor** , si el nuevo inicio de sesión va a ser administrador, haga clic en **sysadmin**; de lo contrario, déjelo en blanco.  
5.  En la página **Asignación de usuarios** , seleccione **Asignar** para la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , si está disponible. Si no lo está, seleccione **master**. Observe que el cuadro **Usuario** se ha rellenado con el inicio de sesión. Al cerrar el cuadro de diálogo, se creará el usuario en la base de datos.  
6.  En el cuadro **Esquema predeterminado** , escriba **dbo** para asignar el inicio de sesión al esquema de propietario de base de datos.   
7.  Acepte los valores predeterminados de los cuadros **Elementos protegibles** y **Estado** y haga clic en **Aceptar** para crear el inicio de sesión.  

> [!IMPORTANT]  
> Esta información es básica para empezar. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona un completo entorno de seguridad y, obviamente, la seguridad es un aspecto importante de las operaciones de base de datos.  

## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Conexión desde otro equipo](../relational-databases/lesson-2-connecting-from-another-computer.md)    
  
