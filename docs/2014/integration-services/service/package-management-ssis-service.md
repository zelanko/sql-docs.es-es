---
title: Administración de paquetes (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dbe4a733479e23e8630e3bbc043ba5dcbf30c1bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091495"
---
# <a name="package-management-ssis-service"></a>Administración de paquetes (servicio SSIS)
  La administración de paquetes implica tareas entre las que se incluyen las siguientes:  
  
-   Supervisar paquetes en ejecución  
  
-   Administrar el almacenamiento de paquetes  
  
-   Importar y exportar paquetes  
  
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
## <a name="package-store"></a>Almacén de paquetes  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona dos carpetas de nivel superior para acceder a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes: **paquetes en ejecución** y **paquetes almacenados**. En la carpeta **Paquetes en ejecución** se muestran los paquetes que se están ejecutando en el servidor. En la carpeta **Paquetes almacenados** se enumeran los paquetes que están guardados en el almacén de paquetes. Estos son los únicos paquetes que administra el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El almacén de paquetes puede constar de la base de datos msdb y las carpetas del sistema de archivos enumeradas en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El archivo de configuración especifica la base de datos msdb y las carpetas del sistema de archivos que se van a administrar. También puede haber paquetes almacenados en otras partes del sistema de archivos que no sean administrados por el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los paquetes que se guardan en msdb quedan almacenados en una tabla denominada sysssispackages. Cuando se guardan paquetes en msdb, también se pueden agrupar en carpetas lógicas. Las carpetas lógicas pueden ayudarle a organizar los paquetes según su fin, o bien a filtrar los paquetes en la tabla sysssispackages. Puede crear carpetas lógicas con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. De manera predeterminada, todas las carpetas lógicas que se agregan a msdb se incluyen automáticamente en el almacén de paquetes.  
  
 Las carpetas lógicas que se crean para agrupar paquetes en msdb se representan como filas en la tabla sysssispackagefolders de msdb. Las columnas folderid y parentfolderid de sysssispackagefolders definen la jerarquía de carpetas. Las carpetas lógicas raíz de msdb son las filas de sysssispackagefolders que tienen valores NULL en la columna parentfolderid. Para más información, vea [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql) y [sysssispackagefolders &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackagefolders-transact-sql).  
  
 Cuando abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y se conecte a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], verá las carpetas de msdb que administra el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enumeradas en la carpeta Paquetes almacenados. Si el archivo de configuración especifica carpetas raíz del sistema de archivos, la carpeta Paquetes almacenados enumera también los paquetes guardados en el sistema de archivos en esas carpetas y en todas las subcarpetas.  
  
 Puede almacenar paquetes en cualquier carpeta del sistema de archivos, pero no aparecerán en las subcarpetas de la carpeta **Paquetes almacenados** a menos que se agregue la carpeta a la lista de carpetas en el archivo de configuración del almacén de paquetes. Para más información sobre el archivo de configuración, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](integration-services-service-ssis-service.md).  
  
 La carpeta **Paquetes en ejecución** no contiene subcarpetas y no es extensible.  
  
 De forma predeterminada, la carpeta **Paquetes almacenados** contiene dos carpetas: **Sistema de archivos** y **MSDB**. En la carpeta **Sistema de archivos** se enumeran los paquetes que se guardan en el sistema de archivos. La ubicación de estos archivos se especifica en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La carpeta predeterminada es la carpeta Paquetes, ubicada en %Archivos de programa%\Microsoft SQL Server\100\DTS. En la carpeta **MSDB** se muestran los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] guardados en la base de datos msdb de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor. La tabla sysssispackages contiene los paquetes que se guardan en msdb.  
  
 Para ver la lista de paquetes del almacén de paquetes, debe abrir [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conectarse a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para más información, vea [View Integration Services Packages in SQL Server Management Studio &#40;SSIS Service&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md).  
  
## <a name="monitoring-running-packages"></a>Supervisar paquetes en ejecución  
 En la carpeta **Paquetes en ejecución** se muestran los paquetes que se están ejecutando en ese momento. Para ver la información acerca de los paquetes actuales en la página **Resumen** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic en la carpeta **Paquetes en ejecución** . En la página **Resumen** se muestra información como la duración de la ejecución de los paquetes. Si lo desea, puede actualizar la carpeta para ver la información más reciente.  
  
 Para ver la información de un solo paquete en ejecución en la página **Resumen** , haga clic en el paquete. En la página **Resumen** se muestra información como la versión y la descripción del paquete.  
  
 Puede detener la ejecución de un paquete de la carpeta **Paquetes en ejecución** si hace clic con el botón derecho en el paquete y luego hace clic en **Detener**.  
  
## <a name="managing-package-storage"></a>Administrar el almacenamiento de paquetes  
 Para organizar paquetes, puede agregar carpetas personalizadas a las carpetas raíz del almacén de paquetes que aparecen en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . De forma predeterminada, las carpetas raíz son las carpetas **Sistema de archivos** y **MSDB** . Por ejemplo, es posible que desee agregar a la carpeta **Sistema de archivos** una carpeta **Limpieza de datos** que contenga todos los paquetes utilizados para la limpieza de datos. Puede agregar carpetas personalizadas a las carpetas personalizadas, creando así una jerarquía de carpetas anidadas adaptada a sus necesidades. Puede eliminar y cambiar el nombre de las carpetas personalizadas, pero no de las carpetas raíz especificadas en el archivo de configuración. Para actualizar las carpetas raíz que aparecen en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , debe actualizar el archivo de configuración.  
  
 Para más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../configuring-the-integration-services-service-ssis-service.md).  
  
## <a name="importing-and-exporting-packages"></a>Importar y exportar paquetes  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] los paquetes se pueden guardar en la base de datos msdb o en el sistema de archivos. Puede copiar un paquete de un tipo de almacenamiento a otro con la característica de importación o exportación que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . También puede importar un paquete al mismo tipo de almacenamiento y asignarle un nombre distinto, para crear una copia de un paquete. La utilidad de símbolo del sistema **dtutil** (dtutil.exe) también se puede usar para importar y exportar paquetes.  
  
 Para más información, consulte [dtutil Utility](../dtutil-utility.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Importar y exportar paquetes &#40;servicio SSIS&#41;](../import-and-export-packages-ssis-service.md)  
  
-   [Ver paquetes en SQL Server Management Studio de Integration Services &#40;servicio SSIS&#41;](../view-integration-services-packages-in-sql-server-management-studio-ssis-service.md)  
  
## <a name="see-also"></a>Vea también  
 [Servicio Integration Services &#40;servicio SSIS&#41;](integration-services-service-ssis-service.md)  
  
  
