---
title: Conectarse a una base de datos de Access | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Access [Integration Services]
- Access databases [Integration Services]
ms.assetid: 229fbd46-ef6a-4609-a4cc-d80d52c33cf1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d82334ca4c5b5efb1d956c8d3a8afe901fc94f83
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-an-access-database"></a>Conectarse a una base de datos de Access
  La conexión de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a un origen de datos de Microsoft Office Access requiere un administrador de conexiones y un proveedor de datos OLE DB. El proveedor de datos que se use dependerá de la versión de Access que creó el origen de datos:  
  
-   En Access 2003 y versiones anteriores, el paquete requiere el proveedor OLE DB para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet.  
  
-   En Access 2007, el paquete requiere el proveedor OLE DB para el motor de base de datos de Microsoft Office Access 12.0.  
  
 Puede crear un administrador de conexiones OLE DB y seleccionar el proveedor de datos correspondiente desde el área de administradores de conexión del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o desde el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  En un equipo de 64 bits, deberá ejecutar paquetes que se conecten a los orígenes de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access en modo de 32 bits. El proveedor OLE DB para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet y el proveedor OLE DB para el motor de base de datos de Microsoft Office Access 12.0 únicamente están disponibles en versiones de 32 bits.  

## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividad para archivos de Microsoft Excel y Access
  
Es posible que tenga que descargar los componentes de conectividad para archivos de Microsoft Office si aún no están instalados. Descargue la versión más reciente de los componentes de conectividad para los archivos de Access y Excel aquí: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir los archivos creados con versiones anteriores de los programas de Access.

Si el equipo tiene una versión de Office de 32 bits, tendrá que instalar la versión de 32 bits de los componentes, y también debe asegurarse de que ejecuta el paquete en el modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de descargar Access Database Engine 2016 Redistributable y no Microsoft Access 2016 Runtime. Al ejecutar el instalador, es posible que vea un mensaje de error que indica que no se puede instalar la descarga en paralelo con componentes para hacer clic y ejecutar de Office. Para omitir este mensaje de error, ejecute la instalación en modo silencioso abriendo una ventana del símbolo del sistema y ejecutando el archivo .EXE que descargó con el modificador `/quiet`. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="connecting-to-a-data-source-in-access-2003-or-earlier-format"></a>Conectar a un origen de datos con el formato de Access 2003 o anterior  
  
### <a name="to-create-an-access-connection-manager-from-the-connection-managers-area"></a>Para crear un administrador de conexiones con Access desde el área de administradores de conexión  
  
1.  Abra el paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y seleccione **Nueva conexión OLE DB**.  
  
3.  En el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** , haga clic en **Nuevo**.  
  
     Para más información, vea [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  En el cuadro de diálogo **Administrador de conexiones** , en **Proveedor**, seleccione **Microsoft Jet 4.0 OLE DB Provider**y, a continuación, configure el administrador de conexiones que corresponda.  
  
### <a name="to-create-an-access-connection-from-the-sql-server-import-and-export-wizard"></a>Para crear una conexión con Access desde el Asistente para importación y exportación de SQL Server  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], inicie el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  En la página **Elegir un origen de datos** , seleccione **Microsoft Access**en **Origen de datos**y, a continuación, configure la conexión con Access.  
  
     Al seleccionar **Microsoft Access** como **Origen de datos**, el asistente creará automáticamente el administrador de conexiones OLE DB necesario con el proveedor de datos correcto. Para más información, vea [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="connecting-to-a-data-source-in-access-2007-format"></a>Conectar a un origen de datos con el formato de Access 2007  
 Para obtener acceso a un origen de datos de Access 2007, el administrador de conexiones OLE DB necesita el proveedor OLE DB para el motor de base de datos de Microsoft Office Access 12.0. Este proveedor se instala automáticamente con 2007 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office system. Si 2007 Office system no está instalado en el equipo en el que se está ejecutando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , deberá instalar el proveedor por separado. Para instalar el proveedor OLE DB para el motor de base de datos de Microsoft Office Access 12.0, descargue e instale los componentes que encontrará en esta página web, [2007 Office System Driver: Data Connectivity Components](http://go.microsoft.com/fwlink/?LinkId=98155).  
  
### <a name="to-create-an-ole-db-connection-manager-from-the-connection-managers-area"></a>Para crear un administrador de conexiones OLE DB desde el área de administradores de conexión  
  
1.  Abra el paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y seleccione **Nueva conexión OLE DB**.  
  
3.  En el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** , haga clic en **Nuevo**.  
  
     Para más información, vea [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
4.  En el cuadro de diálogo **Administrador de conexiones** , en **Proveedor**, seleccione **Microsoft Office 12.0 Access Database Engine OLE DB**y, a continuación, configure el administrador de conexiones que corresponda.  
  
    > [!NOTE]  
    >  Para conectarse a un origen de datos que use Access 2007, no puede seleccionar **Proveedor OLE DB de Microsoft Jet 4.0** como **Origen de datos**.  
  
### <a name="to-create-an-ole-db-connection-from-the-sql-server-import-and-export-wizard"></a>Para crear una conexión OLE DB desde el Asistente para importación y exportación de SQL Server  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], inicie el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  En la página **Elegir un origen de datos** , seleccione **Microsoft Office 12.0 Access Database Engine OLE DB Provider**en **Origen de datos**y, a continuación, configure la conexión que corresponda.  
  
    > [!NOTE]  
    >  Para conectarse a un origen de datos que use Access 2007, no puede seleccionar **Proveedor OLE DB de Microsoft Jet 4.0** como **Origen de datos**.  
  
     Al seleccionar **Microsoft Office 12.0 Access Database Engine OLE DB Provider** como **Origen de datos**, el asistente crea automáticamente el administrador de conexiones OLE DB necesario con el proveedor de datos correcto. Para más información, vea [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
## <a name="see-also"></a>Ver también  
 [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
