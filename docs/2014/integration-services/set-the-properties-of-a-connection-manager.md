---
title: Establecer las propiedades de un administrador de conexiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], modifying
- modifying connection managers
ms.assetid: 54793114-2198-4d80-8091-e241d5a5d13c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92ac3366a2473fb92fe33dcf884d3806c65e8609
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62885567"
---
# <a name="set-the-properties-of-a-connection-manager"></a>Establecer las propiedades de un administrador de conexiones
  Todos los administradores de conexión se pueden configurar en la ventana **Propiedades** .  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] también proporciona cuadros de diálogo personalizados para modificar los distintos tipos de administradores de conexiones en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. El cuadro de diálogo tiene un conjunto de opciones diferente para cada tipo de administrador de conexiones.  
  
### <a name="to-modify-a-connection-manager-using-the-properties-window"></a>Para modificar un administrador de conexiones mediante la ventana Propiedades  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador SSIS, haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexión** .  
  
4.  Haga clic con el botón derecho en el administrador de conexiones y haga clic en **Propiedades**.  
  
5.  En la ventana **Propiedades** , modifique los valores de las propiedades. La ventana **Propiedades** proporciona acceso a algunas propiedades que no se pueden configurar en el editor estándar para un administrador de conexiones.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Para modificar un administrador de conexiones mediante el cuadro de diálogo Administrador de conexiones  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en la pestaña **Flujo de control** , **Flujo de datos** o **Controlador de eventos** para que esté disponible el área **Administradores de conexiones** .  
  
4.  En el área **Administradores de conexiones** , haga doble clic en el administrador de conexiones para abrir el cuadro de diálogo **Administrador de conexiones** . Para obtener información acerca de tipos específicos de administradores de conexión y de las opciones disponibles para cada tipo, vea la tabla siguiente.  
  
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
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md)   
 [Agregar, eliminar o compartir un administrador de conexiones en un paquete](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
  
