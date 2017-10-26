---
title: Conectarse a un libro de Excel | Documentos de Microsoft
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: f8fb1db80ac1b750950a3401516b54af5ee29686
ms.contentlocale: es-es
ms.lasthandoff: 08/17/2017

---
# <a name="connect-to-an-excel-workbook"></a>Conectarse a un libro de Excel
  Para conectar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a un libro de Microsoft Office Excel es necesario disponer de un administrador de conexiones.  
  
 Puede crear estos administradores de conexión desde el área de administradores de conexión en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o desde el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividad para archivos de Microsoft Excel y Access
  
Tendrá que descargar los componentes de conectividad para archivos de Microsoft Office si no están instaladas. Descargar la versión más reciente de los componentes de conectividad para los archivos de Excel y Access aquí: [redistribuible de 2016 de motor de base de datos Microsoft acceso](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir archivos creados con versiones anteriores de Excel.

Si el equipo tiene una versión de 32 bits de Office, tendrá que instalar la versión de 32 bits de los componentes, y también tiene que asegurarse de que se ejecuta el paquete en modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de que descargue el redistribuible de 2016 de motor de base de datos de acceso y no el Runtime de 2016 de Microsoft Access. Al ejecutar el programa de instalación, verá un mensaje de error que no se puede instalar la descarga en paralelo con componentes de hacer clic para ejecutar Office. Para omitir este mensaje de error e instalar los componentes correctamente, ejecute la instalación en modo silencioso, abra una ventana del símbolo del sistema y ejecuta el. Un archivo ejecutable que se descargó con el `/quiet` cambiar. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Crear un administrador de conexiones Excel

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>Para crear un administrador de conexiones con Excel desde el área de administradores de conexión  
  
1.  Abra el paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en cualquier punto del área **Administradores de conexión** y luego seleccione **Nueva conexión**.  
  
3.  En el cuadro de diálogo **Agregar administrador de conexiones SSIS** , seleccione **Excel**y, a continuación, configure el administrador de conexiones.  
  
     Para obtener información sobre las opciones de configuración disponibles para este administrador de conexiones, vea [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>Para crear una conexión con Excel desde el Asistente para importación y exportación de SQL Server  
  
1.  Inicie la versión de 32 bits del Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  En la página **Elegir un origen de datos** , seleccione **Microsoft Excel**en **Origen de datos**y, a continuación, configure la conexión con Excel.  
  
     Para obtener información sobre las opciones de configuración disponibles para este tipo de conexión, vea [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a una base de datos de Access](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  

