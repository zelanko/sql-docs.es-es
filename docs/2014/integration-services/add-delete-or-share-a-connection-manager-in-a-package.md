---
title: Agregar, eliminar o compartir un administrador de conexiones en un paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b7d92800a2f5d55cf85ace3e7746d934b7474b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062011"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>Agregar, eliminar o compartir un administrador de conexiones en un paquete
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye varios tipos de administradores de conexiones para conectar con diferentes orígenes de datos, como bases de datos relacionales, bases de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y archivos en formatos CSV Y XML. Se puede crear un administrador de conexiones en el nivel de paquete o en el nivel de proyecto. El administrador de conexiones creado en el nivel de proyecto está disponible para todos los paquetes del proyecto. En tanto que el administrador de conexiones creado en el nivel de paquete está disponible para ese paquete específico.  
  
 Utilice los administradores de conexiones que se crean en el nivel de proyecto en lugar de orígenes de datos, para compartir conexiones a orígenes. Para agregar un administrador de conexiones en el nivel de proyecto, el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] debe utilizar el modelo de implementación del proyecto. Cuando se configura un proyecto de usar este modelo, la carpeta **Administradores de conexiones** aparece en el **Explorador de soluciones**y la carpeta **Orígenes de datos** se quita del **Explorador de soluciones**.  
  
> [!NOTE]  
>  Si desea utilizar orígenes de datos en el paquete, debe convertir el proyecto en el modelo de implementación de paquetes.  
>   
>  Para obtener más información acerca de los dos modelos, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md). Para obtener más información sobre cómo convertir un proyecto al modelo de implementación de proyectos, vea [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 Los siguientes procedimientos se aplican a todos los tipos de administradores de conexiones y describen cómo realizar las siguientes tareas:  
  
-   [Para agregar un administrador de conexiones al crear un paquete](#wizard)  
  
-   [Para agregar un administrador de conexiones a un paquete existente](#package)  
  
-   [Para agregar un administrador de conexiones en el nivel de proyecto](#project)  
  
-   [Para crear un parámetro para una propiedad del Administrador de conexiones](#parameter)  
  
-   [Para eliminar un administrador de conexiones de un paquete](#DeletePackageLevel)  
  
-   [Para eliminar un administrador de conexiones compartido (Administrador de conexiones de nivel de proyecto)](#DeleteProjectLevel)  
  
##  <a name="wizard"></a> Para agregar un administrador de conexiones al crear un paquete  
  
-   Use el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
     Además de crear y configurar un administrador de conexiones, el asistente también ayuda a crear y configurar los orígenes y destinos que utilizan el administrador de conexiones. Para obtener más información, vea [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
##  <a name="package"></a> Para agregar un administrador de conexiones a un paquete existente  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexiones** .  
  
4.  Haga clic con el botón derecho en cualquier lugar del área **Administradores de conexiones** y, después, siga uno de estos procedimientos:  
  
    -   Haga clic en el tipo de administrador de conexiones que desee agregar al paquete.  
  
         -o bien-  
  
    -   Si no aparece el tipo que desea agregar, haga clic en **Nueva conexión** para abrir el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione un tipo de administrador de conexiones y haga clic en **Aceptar**.  
  
     Se abrirá el cuadro de diálogo personalizado para el tipo de administrador de conexiones seleccionado. Para obtener más información acerca de los tipos de administradores de conexiones y las opciones disponibles, vea la siguiente tabla de opciones.  
  
    |Administrador de conexiones|Opciones|  
    |------------------------|-------------|  
    |[Administrador de conexiones ADO](connection-manager/ado-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configurar el administrador de conexiones ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Administrador de conexiones de Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de Excel](connection-manager/excel-connection-manager.md)|[Editor del administrador de conexiones con Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Administrador de conexiones de archivos](connection-manager/file-connection-manager.md)|[Editor del administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Administrador de conexiones de varios archivos](connection-manager/multiple-files-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de archivos planos](connection-manager/flat-file-connection-manager.md)|[Editor del administrador de conexiones de archivos planos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones de varios archivos planos](connection-manager/multiple-flat-files-connection-manager.md)|[Editor del administrador de conexiones de varios archivos planos &#40;página General&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Columnas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Avanzadas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Vista previa&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones FTP](connection-manager/ftp-connection-manager.md)|[Editor del administrador de conexiones FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Administrador de conexiones HTTP](connection-manager/http-connection-manager.md)|[Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Administrador de conexiones MSMQ](connection-manager/msmq-connection-manager.md)|[Editor del administrador de conexiones MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Administrador de conexiones ODBC](connection-manager/odbc-connection-manager.md)|[Referencia de la interfaz de usuario del administrador de conexiones ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[Administrador de conexiones OLE DB](connection-manager/ole-db-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones SMO](connection-manager/smo-connection-manager.md)|[Editor del administrador de conexiones SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Administrador de conexiones SMTP](connection-manager/smtp-connection-manager.md)|[Editor del administrador de conexiones SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Administrador de conexiones con SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Conexión&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Todo&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Administrador de conexiones WMI](connection-manager/wmi-connection-manager.md)|[Editor del administrador de conexiones WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     En el área **Administradores de conexiones** se muestra el administrador de conexiones agregado.  
  
5.  Opcionalmente, puede hacer clic con el botón derecho en el administrador de conexiones, hacer clic en **Cambiar nombre**y, después, modificar el nombre predeterminado del administrador de conexiones.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** en el menú **Archivo** .  
  
##  <a name="project"></a> Para agregar un administrador de conexiones en el nivel de proyecto  
  
1.  Abra el proyecto de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Administradores de conexiones**y, después, en **Nuevo administrador de conexiones**.  
  
3.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione el tipo de administrador de conexiones y, a continuación, haga clic en **Agregar**.  
  
     Se abrirá el cuadro de diálogo personalizado para el tipo de administrador de conexiones seleccionado. Para obtener más información acerca de los tipos de administradores de conexiones y las opciones disponibles, vea la siguiente tabla de opciones.  
  
    |Administrador de conexiones|Opciones|  
    |------------------------|-------------|  
    |[Administrador de conexiones ADO](connection-manager/ado-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configurar el administrador de conexiones ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Administrador de conexiones de Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de Excel](connection-manager/excel-connection-manager.md)|[Editor del administrador de conexiones con Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Administrador de conexiones de archivos](connection-manager/file-connection-manager.md)|[Editor del administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Administrador de conexiones de varios archivos](connection-manager/multiple-files-connection-manager.md)|[Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de archivos](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Administrador de conexiones de archivos planos](connection-manager/flat-file-connection-manager.md)|[Editor del administrador de conexiones de archivos planos &#40;página General&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Columnas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Avanzadas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de archivos planos &#40;página Vista previa&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones de varios archivos planos](connection-manager/multiple-flat-files-connection-manager.md)|[Editor del administrador de conexiones de varios archivos planos &#40;página General&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Columnas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Avanzadas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor del administrador de conexiones de varios archivos planos &#40;página Vista previa&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Administrador de conexiones FTP](connection-manager/ftp-connection-manager.md)|[Editor del administrador de conexiones FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Administrador de conexiones HTTP](connection-manager/http-connection-manager.md)|[Editor del administrador de conexiones HTTP &#40;página Servidor&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor del administrador de conexiones HTTP &#40;página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Administrador de conexiones MSMQ](connection-manager/msmq-connection-manager.md)|[Editor del administrador de conexiones MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Administrador de conexiones ODBC](connection-manager/odbc-connection-manager.md)|[Referencia de la interfaz de usuario del administrador de conexiones ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[Administrador de conexiones OLE DB](connection-manager/ole-db-connection-manager.md)|[Configurar el administrador de conexiones OLE DB](configure-ole-db-connection-manager.md)|  
    |[Administrador de conexiones SMO](connection-manager/smo-connection-manager.md)|[Editor del administrador de conexiones SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Administrador de conexiones SMTP](connection-manager/smtp-connection-manager.md)|[Editor del administrador de conexiones SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Administrador de conexiones con SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Conexión&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor del administrador de conexiones con SQL Server Compact Edition &#40;página Todo&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Administrador de conexiones WMI](connection-manager/wmi-connection-manager.md)|[Editor del administrador de conexiones WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     El administrador de conexiones que agregó aparecerá en el nodo de **Administradores de conexiones** en el **Explorador de soluciones**. También aparecerá en la pestaña **Administradores de conexiones** de la ventana **Diseñador SSIS** para todos los paquetes del proyecto. El nombre del administrador de conexiones de esta pestaña tendrá el prefijo **(proyecto)** para distinguir este administrador de conexiones de nivel de proyecto de los administradores de conexiones de nivel de paquete.  
  
4.  Si quiere, haga clic con el botón derecho en el administrador de conexiones de la ventana **Explorador de soluciones** en el nodo **Administradores de conexiones** o en la pestaña **Administradores de conexiones** de la ventana **Diseñador SSIS** , haga clic en **Cambiar nombre**y, después, modifique el nombre predeterminado del administrador de conexiones.  
  
    > [!NOTE]  
    >  En la pestaña **Administradores de conexiones** de la ventana **Diseñador SSIS**, no podrá sobrescribir el prefijo **(proyecto)** del nombre del administrador de conexiones. es así por diseño.  
  
##  <a name="parameter"></a> Para crear un parámetro para una propiedad del Administrador de conexiones  
  
1.  En el área de **Administradores de conexiones** , haga clic con el botón derecho en el administrador de conexiones para el que quiere crear un parámetro y haga clic en **Parametrizar**.  
  
2.  Configure los valores de parámetro en el cuadro de diálogo **Parametrizar** . Para más información, consulte [Parameterize Dialog Box](../../2014/integration-services/parameterize-dialog-box.md).  
  
##  <a name="DeletePackageLevel"></a> Para eliminar un administrador de conexiones de un paquete  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexiones** .  
  
4.  Haga clic con el botón derecho en el administrador de conexiones que quiera eliminar y haga clic en **Eliminar**.  
  
     Si elimina un administrador de conexiones que use un elemento de paquete, como una tarea Ejecutar SQL o un origen de OLE DB, experimentará los resultados siguientes:  
  
    -   Un icono de error aparece en el elemento de paquete que usaba el administrador de conexiones eliminado.  
  
    -   El paquete no puede validarse.  
  
    -   El paquete no se puede ejecutar.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
##  <a name="DeleteProjectLevel"></a> Para eliminar un administrador de conexiones compartido (Administrador de conexiones de nivel de proyecto)  
  
1.  Para eliminar un administrador de conexiones de nivel de proyecto, haga clic con el botón derecho en el administrador de conexiones en el nodo **Administradores de conexiones** de la ventana del **Explorador de soluciones** y haga clic en **Eliminar**. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] muestra el siguiente mensaje de advertencia:  
  
    > [!WARNING]  
    >  Si elimina un administrador de conexiones del proyecto, los paquetes que utilizan el administrador de conexiones no pueden ejecutarse. No es posible deshacer esta acción. ¿Desea eliminar el administrador de conexiones?  
  
2.  Haga clic en Aceptar para eliminar el administrador de conexiones o en Cancelar para mantenerlo.  
  
    > [!NOTE]  
    >  También puede eliminar un administrador de conexiones de nivel de proyecto en la pestaña **Administrador de conexiones** de la ventana **Diseñador SSIS** abierta para los paquetes del proyecto. Para ello, haga clic con el botón derecho en el administrador de conexiones en la pestaña y después haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md)   
 [Establecer las propiedades de un administrador de conexiones](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
