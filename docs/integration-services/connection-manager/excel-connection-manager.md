---
title: Administrador de conexiones de Excel | Documentos de Microsoft
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: a5ce75f3c1715870113626642150028e31a0d58b
ms.contentlocale: es-es
ms.lasthandoff: 08/17/2017

---
# <a name="excel-connection-manager"></a>Administrador de conexiones con Excel
  Un Administrador de conexiones con Excel permite a un paquete conectarse con un archivo de libro de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel existente. El origen de Excel y el destino de Excel que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usan el Administrador de conexiones con Excel.  
  
 Al agregar un Administrador de conexiones con Excel a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un Administrador de conexiones que se resuelve como una conexión Excel en el tiempo de ejecución, establece las propiedades del Administrador de conexiones y agrega el Administrador de conexiones a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **EXCEL**.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Configuración del administrador de conexiones de Excel  
 Puede configurar el Administrador de conexiones con Excel de las maneras siguientes:  
  
-   Especificar la ruta del archivo de libro de Excel.  
  
    > [!NOTE]  
    >  No puede conectar con un archivo de Excel protegido mediante contraseña.  
  
-   Especificar la versión de Excel que se usó para crear el archivo.  
  
-   Indicar si la primera fila de datos a los que se tuvo acceso en las hojas de cálculo o los rangos seleccionados contiene nombres de columna.  
  
 Si un origen de Excel utiliza el Administrador de conexiones con Excel, los nombres de las columnas se incluyen con los datos extraídos. Si un destino de Excel utiliza el Administrador de conexiones con Excel, los nombres de las columnas se incluyen con los datos escritos.  
  
 Para más información sobre el comportamiento de los orígenes y destinos de Excel, consulte [Excel Source](../../integration-services/data-flow/excel-source.md) y [Excel Destination](../../integration-services/data-flow/excel-destination.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor de Administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Para más información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
 Para más información sobre cómo crear bucles entre un grupo de archivos de Excel, vea [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="excel-connection-manager-editor"></a>Editor de Administrador de conexiones con Excel
  Utilice el cuadro de diálogo **Editor del administrador de conexiones con Excel** para agregar una conexión a un archivo de libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] existente o nuevo.  
  
 Para obtener más información acerca del Administrador de conexiones con Excel, vea [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
### <a name="options"></a>Opciones  
 **Ruta de acceso del archivo Excel**  
 Escriba la ruta de acceso y el nombre de archivo de un archivo de libro de Excel (.xls) nuevo o existente.  
  
> [!NOTE]  
>  No puede conectar con un archivo de Excel protegido mediante contraseña.  
  
> [!WARNING]  
>  El **Editor de destino de Excel** creará automáticamente el archivo de Excel cuando seleccione una **Conexión de Excel** que señale a un archivo nuevo o inexistente y haga clic en **Nuevo** en **Nombre de la hoja de Excel**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para ir a la carpeta donde se encuentra el archivo de Excel o a la ubicación en la que quiere crear el archivo.  
  
 **Versión de Excel**  
 Especifique la versión de Microsoft Excel utilizada para crear el archivo.  
  
 **La primera fila tiene nombres de columna**  
 Especifique si la primera fila de datos de la hoja seleccionada contiene nombres de columna. El valor predeterminado de esta opción es **True**.  
  
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Componentes de conectividad para archivos de Microsoft Excel y Access
  
Tendrá que descargar los componentes de conectividad para archivos de Microsoft Office si no están instaladas. Descargar la versión más reciente de los componentes de conectividad para los archivos de Excel y Access aquí: [redistribuible de 2016 de motor de base de datos Microsoft acceso](https://www.microsoft.com/download/details.aspx?id=54920).
  
La versión más reciente de los componentes puede abrir archivos creados con versiones anteriores de Excel.

Si el equipo tiene una versión de 32 bits de Office, tendrá que instalar la versión de 32 bits de los componentes, y también tiene que asegurarse de que se ejecuta el paquete en modo de 32 bits.

Si tiene una suscripción de Office 365, asegúrese de que descargue el redistribuible de 2016 de motor de base de datos de acceso y no el Runtime de 2016 de Microsoft Access. Al ejecutar el programa de instalación, verá un mensaje de error que no se puede instalar la descarga en paralelo con componentes de hacer clic para ejecutar Office. Para pasar por alto este mensaje de error, ejecute la instalación en modo silencioso, abra una ventana del símbolo del sistema y ejecuta el. Un archivo ejecutable que se descargó con el `/quiet` cambiar. Por ejemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
-   [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
