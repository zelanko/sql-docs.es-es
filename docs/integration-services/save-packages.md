---
title: Guardar paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e9a2cbb66b7b77a9cb87b779baf76f63f627bd2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542022"
---
# <a name="save-packages"></a>Guardar paquetes
  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , se generan los paquetes con el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y se guardan en el sistema de archivos como archivos XML (archivos .dtsx). También puede guardar copias del archivo XML de paquete en la base de datos msdb, en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o en el almacén de paquetes. El almacén de paquetes representa las carpetas en la ubicación del sistema de archivos que el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administra.  
  
 Si guarda un paquete en el sistema de archivos, puede usar más tarde el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para importar el paquete a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o al almacén de paquetes. Para más información, vea [Servicio Integration Services &#40;servicio SSIS&#41;](../integration-services/service/integration-services-service-ssis-service.md).  
  
 También puede usar una utilidad de símbolo del sistema, **dtutil**, para copiar un paquete entre el sistema de archivos y msdb. Para más información, consulte [dtutil Utility](../integration-services/dtutil-utility.md).  
## <a name="save-a-package-to-the-file-system"></a>Guardar un paquete en el sistema de archivos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea guardar en un archivo.  
  
2.  En el Explorador de soluciones, haga clic en el paquete que desea guardar.  
  
3.  En el menú **Archivo** , haga clic en **Guardar los elementos seleccionados**.  
  
    > [!NOTE]  
    >  Puede comprobar la ruta y el nombre de archivo donde se guardó el paquete en la ventana Propiedades.  

## <a name="save-a-copy-of-a-package"></a>Guardar una copia de un paquete
  En esta sección se describe cómo guardar una copia de un paquete en el sistema de archivos, en el almacén de paquetes o en la base de datos **msdb** en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Al especificar una ubicación para guardar la copia del paquete, puede actualizar también el nombre del paquete.  
  
 El almacén de paquetes puede incluir la base de datos **msdb** y las carpetas del sistema de archivos, solamente la base de datos **msdb**o solamente las carpetas del sistema de archivos. En **msdb**, los paquetes se guardan en la tabla **sysssispackages** . Esta tabla incluye una columna **folderid** que identifica la carpeta lógica a la que pertenece el paquete. Las carpetas lógicas proporcionan una forma útil de agrupar paquetes guardados en **msdb** del mismo modo que las carpetas del sistema de archivos proporcionan una forma de agrupar paquetes guardados en el sistema de archivos. Las filas en la tabla **sysssispackagefolders** en **msdb** definen las carpetas.  
  
 Si **msdb** no está definida como parte del almacén de paquetes, puede continuar asociando paquetes con carpetas lógicas existentes cuando seleccione SQL Server en la opción **Ruta de acceso del paquete** .  
  
> [!NOTE]  
>  El paquete se debe abrir en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] para poder guardar una copia del paquete.  
  
### <a name="to-save-a-copy-of-a-package"></a>Para guardar una copia de un paquete  
  
1.  En el Explorador de soluciones, haga doble clic en el paquete cuya copia desea guardar.  
  
2.  En el menú **Archivo**, haga clic en **Guardar copia de \<archivo de paquete> como**.  
  
3.  En el cuadro de diálogo **Guardar copia del paquete** , seleccione una ubicación de paquete en la lista **Ubicación del paquete** . Las siguientes opciones están disponibles:  
    -   SQL Server
    -   Sistema de archivos 
    -   Almacén de paquetes SSIS 
  
4.  Si la ubicación es **SQL Server** o **Almacén de paquetes SSIS**, proporcione un nombre de servidor.  
  
5.  Si se guarda en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], especifique el tipo de autenticación y, si se usa la Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione un nombre de usuario y una contraseña.  
  
6.  Para especificar la ruta de acceso del paquete, escríbala o haga clic en el botón Examinar **(…)** para especificar la ubicación del paquete. El nombre predeterminado del paquete es Paquete. Opcionalmente, cambie el nombre del paquete a uno que satisfaga sus necesidades.  
  
     Si selecciona **SQL Server** como opción de **Ruta de acceso del paquete** , la ruta de acceso del paquete consta de carpetas lógicas de **msdb** y el nombre del paquete. Por ejemplo, si el paquete DownloadMonthlyData está asociado con la carpeta Finance dentro de la carpeta MSDB (nombre predeterminado de la carpeta lógica raíz de **msdb**), la ruta del paquete DownloadMonthlyData es MSDB/Finance/DownloadMonthlyData.  
  
     Si selecciona **Almacén de paquetes SSIS** como opción de **Ruta de acceso del paquete** , la ruta del paquete consta de la carpeta que administra el servicio Integration Services. Por ejemplo, si el paquete UpdateDeductions se encuentra en la carpeta HumanResources dentro de la carpeta del sistema de archivos que administra el servicio, la ruta del paquete es /File System/HumanResources/UpdateDeductions; de igual modo, si el paquete PostResumes está asociado con la carpeta HumanResources dentro de la carpeta MSDB, la ruta de acceso del paquete es MSDB/HumanResources/PostResumes.  
  
     Si selecciona **Sistema de archivos** como opción de **Ruta de acceso del paquete** , la ruta del paquete es la ubicación en el sistema de archivos y el nombre de archivo. Por ejemplo, si el nombre del paquete es UpdateDemographics, la ruta del paquete es C:\HumanResources\Quarterly\UpdateDemographics.dtsx.  
  
7.  Revise el nivel de protección del paquete.  
  
8.  También puede hacer clic en el botón Examinar **(…)** junto al cuadro **Nivel de protección** para cambiar el nivel de protección.  
  
    -   En el cuadro de diálogo **Nivel de protección de paquetes** , seleccione un nivel de protección diferente.  
  
    -   Haga clic en **Aceptar**.  
  
9. Haga clic en **Aceptar**.  

## <a name="save-a-package-as-a-package-template"></a>Guardar un paquete como una plantilla de paquete
 En esta sección se describe cómo designar y usar paquetes personalizados como plantillas cuando se crean nuevos paquetes de Integration Services en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. De forma predeterminada, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa una plantilla de paquetes que crea un paquete vacío cuando se agrega un nuevo paquete a un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . No puede reemplazar esta plantilla predeterminada, pero puede agregar nuevas plantillas.  
  
 Puede designar varios paquetes para utilizar como plantillas. Para poder implementar paquetes personalizados como plantillas, primero debe crear los paquetes.  
  
 Cuando crea paquetes a partir de paquetes personalizados utilizados como plantillas, los nuevos paquetes tienen el mismo nombre y GUID que la plantilla. Para diferenciar los paquetes, debe actualizar el valor de la propiedad **Name** y generar un nuevo GUID para la propiedad **ID** . Para más información, vea [Crear paquetes en herramientas de datos de SQL Server](../integration-services/create-packages-in-sql-server-data-tools.md) y [Establecer las propiedades de paquetes](../integration-services/set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>Para designar un paquete personalizado como plantilla de paquetes  
  
1.  En el sistema de archivos, busque el paquete que desea utilizar como plantilla.  
  
2.  Copie el paquete a la carpeta DataTransformationItems. De forma predeterminada, esta carpeta se encuentra en C:\Archivos de programa\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Repita los pasos 1 y 2 para los demás paquetes que desee utilizar como plantilla.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>Para utilizar un paquete personalizado como plantilla de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que desea crear un paquete.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, seleccione **Agregar** y, después, haga clic en **Nuevo elemento**.  
  
3.  En el cuadro de diálogo **Agregar nuevo elemento -\<nombre de proyecto>**, haga clic en el paquete que quiera usar como plantilla.  
  
     La lista de plantillas incluye la plantilla de paquetes predeterminada denominada Nuevo paquete de SSIS. El icono de paquete identifica plantillas que se pueden utilizar como plantillas de paquetes.  
  
4.  Haga clic en **Agregar**.  
