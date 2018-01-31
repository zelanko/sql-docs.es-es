---
title: Conectarse a un libro de Excel | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3ece6c4ef032f7b60f82f3f58ee602d0a4ac1196
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-excel-workbook"></a>Conectarse a un libro de Excel
  Para conectar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a un libro de Microsoft Office Excel es necesario disponer de un administrador de conexiones.  
  
 Puede crear estos administradores de conexión desde el área de administradores de conexión en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o desde el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividad para archivos de Microsoft Excel y Access
  
Es posible que tenga que descargar los componentes de conectividad para archivos de Microsoft Office si aún no están instalados. Descargue la versión más reciente de los componentes de conectividad para los archivos de Access y Excel aquí: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir los archivos creados con versiones anteriores de los programas de Excel.

Si el equipo tiene una versión de Office de 32 bits, tendrá que instalar la versión de 32 bits de los componentes, y también debe asegurarse de que ejecuta el paquete en el modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de descargar Access Database Engine 2016 Redistributable y no Microsoft Access 2016 Runtime. Al ejecutar el instalador, es posible que vea un mensaje de error que indica que no se puede instalar la descarga en paralelo con componentes para hacer clic y ejecutar de Office. Para omitir este mensaje de error e instalar los componentes correctamente, ejecute la instalación en modo silencioso abriendo una ventana del símbolo del sistema y ejecute el archivo .EXE que descargó con el modificador `/quiet`. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Crear un administrador de conexiones con Excel

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>Para crear un administrador de conexiones con Excel desde el área de administradores de conexión  
  
1.  Abra el paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y luego seleccione **Nueva conexión**.  
  
3.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **Excel**y, a continuación, configure el administrador de conexiones.  
  
     Para obtener información sobre las opciones de configuración disponibles para este administrador de conexiones, vea [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>Para crear una conexión con Excel desde el Asistente para importación y exportación de SQL Server  
  
1.  Inicie la versión de 32 bits del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  En la página **Elegir un origen de datos** , seleccione **Microsoft Excel**en **Origen de datos**y, a continuación, configure la conexión con Excel.  
  
     Para obtener información sobre las opciones de configuración disponibles para este tipo de conexión, vea [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## <a name="see-also"></a>Ver también  
 [Conectarse a una base de datos de Access](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  
