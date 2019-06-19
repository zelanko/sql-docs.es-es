---
title: Administración de paquetes (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6d4d453c1e5c6de342ac81fdd828a570bdc33e5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65805267"
---
# <a name="package-management-ssis-service"></a>Administración de paquetes (servicio SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La administración de paquetes incluye la supervisión, administración, importación y exportación de paquetes.  
 
 ## <a name="package-store"></a>Almacén de paquetes  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona dos carpetas de nivel superior para tener acceso a paquetes: 
 - **Paquetes en ejecución** 
 - **Paquetes almacenados**

 En la carpeta **Paquetes en ejecución** se muestran los paquetes que se están ejecutando en el servidor. En la carpeta **Paquetes almacenados** se enumeran los paquetes que están guardados en el almacén de paquetes. Estos son los únicos paquetes que administra el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El almacén de paquetes puede constar de la base de datos msdb y las carpetas del sistema de archivos enumeradas en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El archivo de configuración especifica la base de datos msdb y las carpetas del sistema de archivos que se van a administrar. También puede haber paquetes almacenados en otras partes del sistema de archivos que no sean administrados por el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los paquetes que guarda en msdb quedan almacenados en una tabla denominada sysssispackages. Cuando guarda paquetes en msdb, puede agruparlos en carpetas lógicas. Las carpetas lógicas pueden ayudarle a organizar los paquetes según su fin, o bien a filtrar los paquetes en la tabla sysssispackages. Puede crear carpetas lógicas con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. De manera predeterminada, todas las carpetas lógicas que se agregan a msdb se incluyen automáticamente en el almacén de paquetes.  
  
 Las carpetas lógicas que crea se representan como filas en la tabla sysssispackagefolders de msdb. Las columnas folderid y parentfolderid de sysssispackagefolders definen la jerarquía de carpetas. Las carpetas lógicas raíz de msdb son las filas de sysssispackagefolders con valores NULL en la columna parentfolderid. Para más información, vea [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md) y [sysssispackagefolders (Transact-SQL)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md).  
  
 Cuando abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y se conecte a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], verá las carpetas de msdb que administra el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enumeradas en la carpeta Paquetes almacenados. Si el archivo de configuración especifica carpetas raíz del sistema de archivos, la carpeta Paquetes almacenados enumera también los paquetes guardados en el sistema de archivos en esas carpetas y en todas las subcarpetas.  
  
 Puede almacenar paquetes en cualquier carpeta del sistema de archivos, pero no aparecerán en las subcarpetas de la carpeta **Paquetes almacenados** a menos que se agregue la carpeta a la lista de carpetas en el archivo de configuración del almacén de paquetes. Para más información sobre el archivo de configuración, vea [Servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 La carpeta **Paquetes en ejecución** no contiene subcarpetas y no es extensible.  
  
 De forma predeterminada, la carpeta **Paquetes almacenados** contiene dos carpetas: **Sistema de archivos** y **MSDB**. En la carpeta **Sistema de archivos** se enumeran los paquetes que se guardan en el sistema de archivos. La ubicación de estos archivos se especifica en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La carpeta predeterminada es la carpeta Paquetes, ubicada en %Archivos de programa%\Microsoft SQL Server\100\DTS. En la carpeta **MSDB** se muestran los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] guardados en la base de datos msdb de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor. La tabla sysssispackages contiene los paquetes que se guardan en msdb.  
  
 Para ver la lista de paquetes del almacén de paquetes, debe abrir [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="monitor-running-packages"></a>Supervisión de paquetes en ejecución  
 En la carpeta **Paquetes en ejecución** se muestran los paquetes que se están ejecutando en ese momento. Para ver la información acerca de los paquetes actuales en la página **Resumen** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic en la carpeta **Paquetes en ejecución** . En la página **Resumen** se muestra información como la duración de la ejecución de los paquetes. Si lo desea, puede actualizar la carpeta para ver la información más reciente.  
  
 Para ver la información de un solo paquete en ejecución en la página **Resumen** , haga clic en el paquete. En la página **Resumen** se muestra información como la versión y la descripción del paquete.  
  
Para detener la ejecución de un paquete de la carpeta **Paquetes en ejecución**, haga clic con el botón derecho en el paquete y luego haga clic en **Detener**.  
  
## <a name="view-packages-in-ssms"></a>Visualización de paquetes en SSMS
    
 En este procedimiento se explica cómo conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y ver una lista de los paquetes que administra el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
### <a name="to-connect-to-integration-services"></a>Para conectarse a Integration Services  
  
1.  Haga clic en **Inicio**, elija **Todos los programas**, **Microsoft SQL Server**y, a continuación, haga clic en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , seleccione **Integration Services** en la lista **Tipo de servidor** , proporcione un nombre de servidor en el cuadro **Nombre de servidor** y haga clic en **Conectar**.  
  
    > [!IMPORTANT]  
    >  Si no puede conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], es probable que no se esté ejecutando el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para conocer el estado del servicio, haga clic en **Inicio**, elija sucesivamente **Todos los programas**, **Microsoft SQL Server**, **Herramientas de configuración**, y haga clic en **Administrador de configuración de SQL Server**. En el panel izquierdo, haga clic en **Servicios de SQL Server**. En el panel derecho, busque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Inicie el servicio, si no se está ejecutando todavía.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . De forma predeterminada, la ventana del Explorador de objetos está abierta y colocada en la esquina inferior izquierda del estudio. Si el Explorador de objetos no está abierto, haga clic en **Explorador de objetos** en el menú **Ver** .  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>Para ver los paquetes que administra el servicio Integration Services  
  
1.  En el Explorador de objetos, expanda la carpeta Paquetes almacenados.  
  
2.  Expanda las subcarpetas de Paquetes almacenados para mostrar los paquetes.  

## <a name="import-and-export-packages"></a>Importación y ejecución de paquetes
 
 Los paquetes se pueden guardar tanto en la tabla sysssispackages como en la base de datos msdb de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en el sistema de archivos.  
  
 El almacén de paquetes, que es el almacén lógico que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supervisa y administra, puede incluir tanto la base de datos msdb como las carpetas del sistema de archivos especificadas en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Puede importar y exportar paquetes entre los siguientes tipos de almacenamiento:  
  
-   Carpetas del sistema de archivos en cualquier lugar del sistema de archivos.  
  
-   Carpetas del almacén de paquetes SSIS. Las dos carpetas predeterminadas se llaman Sistema de archivos y MSDB.  
  
-   La base de datos msdb de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite importar y exportar paquetes y, a través de estos procesos, cambiar el formato de almacenamiento y la ubicación de los paquetes. Con las características de importación y exportación, puede agregar paquetes al sistema de archivos, al almacén de paquetes o a la base de datos msdb, así como copiar paquetes de un formato de almacenamiento a otro. Por ejemplo, los paquetes guardados en msdb se pueden copiar al sistema de archivos y viceversa.  
  
 También puede copiar un paquete a un formato distinto con la utilidad del símbolo del sistema **dtutil** (dtutil.exe). Para más información, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
 Puede importar o exportar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de las ubicaciones siguientes o a dichas ubicaciones:  
  
-   Puede importar un paquete que esté almacenado en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en el sistema de archivos, o en el almacén de paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] . El paquete importado se guarda en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en una carpeta del almacén de paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   Puede exportar un paquete que esté almacenado en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en el sistema de archivos, o en el almacén de paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] a una ubicación y un formato de almacenamiento diferentes.  
  
 Sin embargo, hay algunas restricciones en la importación y exportación de un paquete entre versiones diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   En una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], puede importar paquetes de una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], pero no puede exportar paquetes a una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
-   En una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], no puede importar paquetes de una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]o exportar paquetes a dicha instancia.  
  
 Los procedimientos siguientes describen cómo utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para importar o exportar un paquete.  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>Para importar un paquete con SQL Server Management Studio  
  
1.  Haga clic en **Inicio**, seleccione **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, después, haga clic en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar con el servidor** establezca las opciones siguientes:  
  
    -   En el cuadro **Tipo de servidor** , seleccione **Integration Services**.  
  
    -   En el cuadro **Nombre del servidor**, escriba un nombre de servidor o haga clic en **\<Buscar más…>** y busque el servidor que quiera usar.  
  
3.  Si el Explorador de objetos no está abierto, en el menú **Ver** , haga clic en **Explorador de objetos**.  
  
4.  En el Explorador de objetos, expanda la carpeta **Paquetes almacenados** .  
  
5.  Expanda las subcarpetas para encontrar la carpeta en la que desea importar un paquete.  
  
6.  Haga clic con el botón derecho en la carpeta, haga clic en **Importar paquete**. y, a continuación, realice una de las acciones siguientes:  
  
    -   Para importar desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione la opción **SQL Server** y luego especifique el servidor y seleccione el modo de autenticación. Si selecciona Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione un nombre de usuario y una contraseña.  
  
         Haga clic en el botón Examinar **(…)** , seleccione el paquete que quiera importar y, después, haga clic en **Aceptar**.  
  
    -   Para importar desde el sistema de archivos, seleccione la opción **Sistema de archivos** .  
  
         Haga clic en el botón Examinar **(…)** , seleccione el paquete que quiera importar y, después, haga clic en **Abrir**.  
  
    -   Para importar desde el almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , seleccione la opción **Almacén de paquetes SSIS** y especifique el servidor.  
  
         Haga clic en el botón Examinar **(…)** , seleccione el paquete que quiera importar y, después, haga clic en **Aceptar**.  
  
7.  Si lo desea, actualice el nombre del paquete.  
  
8.  Para actualizar el nivel de protección del paquete, haga clic en el botón Examinar **(…)** y seleccione otro nivel de protección con el cuadro de diálogo **Nivel de protección de paquetes**. Si se selecciona la opción **Cifrar la información confidencial con una contraseña** o la opción **Cifrar todos los datos con una contraseña** , escriba y confirme una contraseña.  
  
9. Haga clic en **Aceptar** para completar la importación.  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>Para exportar un paquete con SQL Server Management Studio  
  
1.  Haga clic en **Inicio**, seleccione **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, después, haga clic en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , establezca las siguientes opciones:  
  
    -   En el cuadro **Tipo de servidor** , seleccione **Integration Services**.  
  
    -   En el cuadro **Nombre del servidor**, escriba un nombre de servidor o haga clic en **\<Buscar más…>** y busque el servidor que quiera usar.  
  
3.  Si el Explorador de objetos no está abierto, en el menú **Ver** , haga clic en **Explorador de objetos**.  
  
4.  En el Explorador de objetos, expanda la carpeta **Paquetes almacenados** .  
  
5.  Expanda las subcarpetas para buscar el paquete que desea exportar.  
  
6.  Opcionalmente, haga clic en **Exportar**y, después, realice una de las operaciones siguientes:  
  
    -   Para exportar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione la opción **SQL Server** y luego especifique el servidor y seleccione el modo de autenticación. Si selecciona Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione un nombre de usuario y una contraseña.  
  
         Haga clic en el botón Examinar **(…)** y expanda la carpeta **Paquetes SSIS** para buscar la carpeta donde quiera guardar el paquete. Opcionalmente, actualice el nombre predeterminado del paquete y luego haga clic en **Aceptar**.  
  
    -   Para exportar al sistema de archivos, seleccione la opción **Sistema de archivos** .  
  
         Haga clic en el botón Examinar **(…)** para buscar la carpeta donde quiera exportar el paquete, escriba el nombre del archivo de paquete y, después, haga clic en **Guardar**.  
  
    -   Para exportar al almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , seleccione la opción **Almacén de paquetes SSIS** y especifique el servidor.  
  
         Haga clic en el botón Examinar **(…)** , expanda la carpeta **Paquetes SSIS** y seleccione la carpeta donde quiera guardar el paquete. Opcionalmente, escriba un nuevo nombre para el paquete en el cuadro de texto **Nombre del paquete** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Para actualizar el nivel de protección del paquete, haga clic en el botón Examinar **(…)** y seleccione otro nivel de protección con el cuadro de diálogo **Nivel de protección de paquetes**. Si se selecciona la opción **Cifrar la información confidencial con una contraseña** o la opción **Cifrar todos los datos con una contraseña** , escriba y confirme una contraseña.  
  
8.  Haga clic en **Aceptar** para completar la exportación.  

## <a name="import-package-dialog-box-ui-reference"></a>Referencia de la interfaz de usuario del cuadro de diálogo Importar paquete
  Utilice el cuadro de diálogo **Importar paquete** , disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para importar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y para establecer o modificar el nivel de protección del paquete.  
  
### <a name="options"></a>Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de ubicación de almacenamiento a la que se importará el paquete. Las siguientes opciones están disponibles:  
  
 **SQL Server**  
  
 **Sistema de archivos**  
  
 **Almacén de paquetes SSIS**  
  
 **Server**  
 Escriba un nombre de servidor o seleccione un servidor de la lista.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción solo está disponible si la ubicación de almacenamiento es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Tipo de autenticación**  
 Seleccione un tipo de autenticación.  
  
 **User name**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete, o bien haga clic en el botón Examinar **(…)** y busque el paquete.  
  
 **Nombre del paquete**  
 También puede cambiar el nombre del paquete si lo desea. El nombre predeterminado es el nombre del paquete que se importará.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y, en el cuadro de diálogo **Nivel de protección de paquetes**, actualice el nivel de protección. Para obtener más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="export-package-dialog-box-ui-reference"></a>Referencia de la interfaz de usuario del cuadro de diálogo Exportar paquete
  Utilice el cuadro de diálogo **Exportar paquete** , disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para exportar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a una ubicación diferente y, opcionalmente, modificar el nivel de protección del paquete.  
  
### <a name="options"></a>Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de almacenamiento al que desea exportar el paquete. Las siguientes opciones están disponibles:  
  
 **SQL Server**  
  
 **Sistema de archivos**  
  
 **Almacén de paquetes SSIS**  
  
 **Server**  
 Escriba un nombre de servidor o seleccione un servidor de la lista.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción solo está disponible si la ubicación de almacenamiento es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Tipo de autenticación**  
 Seleccione un tipo de autenticación.  
  
 **User name**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete, o bien haga clic en el botón Examinar **(…)** y busque la carpeta donde quiera guardar el paquete.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y actualice el nivel de protección en el cuadro de diálogo **Nivel de protección de paquetes**. Para obtener más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="back-up-and-restore-packages"></a>Copia de seguridad y restauración de paquetes
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes se pueden guardar en el sistema de archivos o en msdb, una base de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se puede crear una copia de seguridad de los paquetes guardados en msdb y restaurarlos con las características de copia de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para más información sobre la copia de seguridad y la restauración de la base de datos msdb, haga clic en uno de los temas siguientes:  
  
-   [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye la utilidad del símbolo del sistema **dtutil** (dtutil.exec), que puede usarse para administrar paquetes. Para más información, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="configuration-files"></a>Archivos de configuración  
 Todos los archivos de configuración incluidos en los paquetes se almacenan en el sistema de archivos. Estos archivos no se incluyen en la copia de seguridad de la base de datos msdb; por lo tanto, debe crear periódicamente una copia de seguridad de los archivos de configuración como parte del plan para proteger los paquetes guardados en msdb. Para incluir las configuraciones en la copia de seguridad de la base de datos msdb, puede usar el tipo de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en lugar de las configuraciones basadas en archivos.  
  
### <a name="packages-stored-in-the-file-system"></a>Paquetes almacenados en el sistema de archivos  
 La copia de seguridad de los paquetes guardados en el sistema de archivos debe incluirse en el plan de copia de seguridad del sistema de archivos del servidor. El archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que tiene el nombre predeterminado MsDtsSrvr.ini.xml, contiene una lista de las carpetas del servidor que supervisa el servicio. Debe asegurarse de que se cree la copia de seguridad de estas carpetas. Además, los paquetes se pueden almacenar en otras carpetas del servidor y debe asegurarse de incluir estas carpetas en la copia de seguridad.  

## <a name="see-also"></a>Consulte también  
 [Servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  
