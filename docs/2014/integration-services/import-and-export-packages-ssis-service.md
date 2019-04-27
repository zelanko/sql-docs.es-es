---
title: Importar y exportar paquetes (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0ff095819fc4bdd985ebd083eb09056aa5259322
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768244"
---
# <a name="import-and-export-packages-ssis-service"></a>Importar y exportar paquetes (servicio SSIS)
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 Los paquetes se pueden guardar tanto en la tabla sysssispackages como en la base de datos msdb de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o en el sistema de archivos.  
  
 El almacén de paquetes, que es el almacén lógico que el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] supervisa y administra, puede incluir tanto la base de datos msdb como las carpetas del sistema de archivos especificadas en el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Puede importar y exportar paquetes entre los siguientes tipos de almacenamiento:  
  
-   Carpetas del sistema de archivos en cualquier lugar del sistema de archivos.  
  
-   Carpetas del almacén de paquetes SSIS. Las dos carpetas predeterminadas se llaman Sistema de archivos y MSDB.  
  
-   La base de datos msdb de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permite importar y exportar paquetes y, a través de estos procesos, cambiar el formato de almacenamiento y la ubicación de los paquetes. Con las características de importación y exportación, puede agregar paquetes al sistema de archivos, al almacén de paquetes o a la base de datos msdb, así como copiar paquetes de un formato de almacenamiento a otro. Por ejemplo, los paquetes guardados en msdb se pueden copiar al sistema de archivos y viceversa.  
  
 También puede copiar un paquete a un formato distinto con la utilidad del símbolo del sistema **dtutil** (dtutil.exe). Para más información, consulte [dtutil Utility](dtutil-utility.md).  
  
## <a name="to-import-or-export-a-package"></a>Para importar o exportar un paquete  
  
> [!IMPORTANT]  
>  En este tema se describe el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que forma parte de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] admite el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] por motivos de compatibilidad con [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Para más información sobre la administración de paquetes en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], vea [Integration Services &#40;SSIS&#41; Server](catalog/integration-services-ssis-server-and-catalog.md).  
  
 Puede importar o exportar un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de las ubicaciones siguientes o a dichas ubicaciones:  
  
-   Puede importar un paquete que esté almacenado en una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], en el sistema de archivos, o en el almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] . El paquete importado se guarda en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o en una carpeta del almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Puede exportar un paquete que esté almacenado en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], en el sistema de archivos, o en el almacén de paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] a una ubicación y un formato de almacenamiento diferentes.  
  
 Sin embargo, hay algunas restricciones en la importación y exportación de un paquete entre versiones diferentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   En una instancia de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], puede importar paquetes de una instancia de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], pero no puede exportar paquetes a una instancia de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)].  
  
-   En una instancia de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], no puede importar paquetes de una instancia de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]o exportar paquetes a dicha instancia.  
  
 Los procedimientos siguientes describen cómo utilizar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para importar o exportar un paquete.  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>Para importar un paquete con SQL Server Management Studio  
  
1.  Haga clic en **Inicio**, seleccione **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y, después, haga clic en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar con el servidor** establezca las opciones siguientes:  
  
    -   En el cuadro **Tipo de servidor** , seleccione **Integration Services**.  
  
    -   En el cuadro **Nombre del servidor**, escriba un nombre de servidor o haga clic en **\<Buscar más…>** y busque el servidor que quiera usar.  
  
3.  Si el Explorador de objetos no está abierto, en el menú **Ver** , haga clic en **Explorador de objetos**.  
  
4.  En el Explorador de objetos, expanda la carpeta **Paquetes almacenados** .  
  
5.  Expanda las subcarpetas para encontrar la carpeta en la que desea importar un paquete.  
  
6.  Haga clic con el botón derecho en la carpeta, haga clic en **Importar paquete**. y, a continuación, realice una de las acciones siguientes:  
  
    -   Para importar desde una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], seleccione la opción **SQL Server** y luego especifique el servidor y seleccione el modo de autenticación. Si selecciona Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione un nombre de usuario y una contraseña.  
  
         Haga clic en el botón Examinar **(…)**, seleccione el paquete que quiera importar y, después, haga clic en **Aceptar**.  
  
    -   Para importar desde el sistema de archivos, seleccione la opción **Sistema de archivos** .  
  
         Haga clic en el botón Examinar **(…)**, seleccione el paquete que quiera importar y, después, haga clic en **Abrir**.  
  
    -   Para importar desde el almacén de paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] , seleccione la opción **Almacén de paquetes SSIS** y especifique el servidor.  
  
         Haga clic en el botón Examinar **(…)**, seleccione el paquete que quiera importar y, después, haga clic en **Aceptar**.  
  
7.  Si lo desea, actualice el nombre del paquete.  
  
8.  Para actualizar el nivel de protección del paquete, haga clic en el botón Examinar **(…)** y seleccione otro nivel de protección con el cuadro de diálogo **Nivel de protección de paquetes**. Si se selecciona la opción **Cifrar la información confidencial con una contraseña** o la opción **Cifrar todos los datos con una contraseña** , escriba y confirme una contraseña.  
  
9. Haga clic en **Aceptar** para completar la importación.  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>Para exportar un paquete con SQL Server Management Studio  
  
1.  Haga clic en **Inicio**, seleccione **Microsoft** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y, después, haga clic en **SQL Server Management Studio**.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , establezca las siguientes opciones:  
  
    -   En el cuadro **Tipo de servidor** , seleccione **Integration Services**.  
  
    -   En el cuadro **Nombre del servidor**, escriba un nombre de servidor o haga clic en **\<Buscar más…>** y busque el servidor que quiera usar.  
  
3.  Si el Explorador de objetos no está abierto, en el menú **Ver** , haga clic en **Explorador de objetos**.  
  
4.  En el Explorador de objetos, expanda la carpeta **Paquetes almacenados** .  
  
5.  Expanda las subcarpetas para buscar el paquete que desea exportar.  
  
6.  Opcionalmente, haga clic en **Exportar**y, después, realice una de las operaciones siguientes:  
  
    -   Para exportar a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], seleccione la opción **SQL Server** y luego especifique el servidor y seleccione el modo de autenticación. Si selecciona Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione un nombre de usuario y una contraseña.  
  
         Haga clic en el botón Examinar **(…)** y expanda la carpeta **Paquetes SSIS** para buscar la carpeta donde quiera guardar el paquete. Opcionalmente, actualice el nombre predeterminado del paquete y luego haga clic en **Aceptar**.  
  
    -   Para exportar al sistema de archivos, seleccione la opción **Sistema de archivos** .  
  
         Haga clic en el botón Examinar **(…)** para buscar la carpeta donde quiera exportar el paquete, escriba el nombre del archivo de paquete y, después, haga clic en **Guardar**.  
  
    -   Para exportar al almacén de paquetes [!INCLUDE[ssIS](../includes/ssis-md.md)] , seleccione la opción **Almacén de paquetes SSIS** y especifique el servidor.  
  
         Haga clic en el botón Examinar **(…)**, expanda la carpeta **Paquetes SSIS** y seleccione la carpeta donde quiera guardar el paquete. Opcionalmente, escriba un nuevo nombre para el paquete en el cuadro de texto **Nombre del paquete** . [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Para actualizar el nivel de protección del paquete, haga clic en el botón Examinar **(…)** y seleccione otro nivel de protección con el cuadro de diálogo **Nivel de protección de paquetes**. Si se selecciona la opción **Cifrar la información confidencial con una contraseña** o la opción **Cifrar todos los datos con una contraseña** , escriba y confirme una contraseña.  
  
8.  Haga clic en **Aceptar** para completar la exportación.  
  
## <a name="see-also"></a>Vea también  
 [Administración de paquetes &#40;servicio SSIS&#41;](service/package-management-ssis-service.md)  
  
  
