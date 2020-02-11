---
title: Habilitar el registro de paquetes en SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ef64ee84a90a74d2206fa8cc766e45b1a691566
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059279"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>Habilitar el registro de paquetes en SQL Server Data Tools
  Este procedimiento describe cómo agregar registros a un paquete, configurar el registro en el nivel de paquete y guardar la configuración de registro en un archivo XML. Solo puede agregar registros en el nivel de paquete, pero el paquete no tiene que realizar registros para habilitar el registro en los contenedores que incluye.  
  
> [!IMPORTANT]  
>  Si implementa el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , el nivel de registro que establezca para la ejecución de paquetes invalidará el registro de paquetes que se configura mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 De manera predeterminada, los contenedores del paquete utilizan la misma configuración de registro que el contenedor principal. Para obtener información sobre la configuración de las opciones de registro para contenedores concretos, vea [Configurar el registro utilizando un archivo de configuración guardado](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md).  
  
### <a name="to-enable-logging-in-a-package"></a>Para habilitar el registro en un paquete  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el menú **SSIS** , haga clic en **Registro**.  
  
3.  Seleccione un proveedor de registro en la lista **Tipo de proveedor** y a continuación, haga clic en **Agregar**.  
  
4.  En la columna **Configuración**, seleccione un administrador de conexiones o haga clic en **\<Nueva conexión>** para crear un nuevo administrador de conexiones del tipo apropiado para el proveedor de registro. En función del proveedor seleccionado, utilice uno de los siguientes administradores de conexión:  
  
    -   Para archivos de texto, utilice un administrador de conexiones de archivos. Para obtener más información, vea [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md) .  
  
    -   Para el [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], utilice un administrador de conexiones de archivos.  
  
    -   Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], utilice un administrador de conexiones OLE DB. Para más información, consulte [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md).  
  
    -   Para el registro de eventos de Windows no haga nada. [!INCLUDE[ssIS](../includes/ssis-md.md)]crea automáticamente el registro.  
  
    -   Para archivos XML, utilice un administrador de conexiones de archivos.  
  
5.  Repita los pasos 3 y 4 para cada registro que desee utilizar en el paquete.  
  
    > [!NOTE]  
    >  Un paquete puede utilizar más de un registro de cada tipo.  
  
6.  Opcionalmente, active la casilla de nivel de paquete, seleccione los registros que quiera usar para el registro de nivel de paquete y, después, haga clic en la pestaña **Detalles** .  
  
7.  En la pestaña **Detalles** , seleccione **Eventos** para registrar todas las entradas del registro o bien, borre **Eventos** para seleccionar eventos concretos.  
  
8.  Opcionalmente, haga clic en **Avanzada** para especificar la información que desee registrar.  
  
    > [!NOTE]  
    >  De manera predeterminada, se registra toda la información.  
  
9. En la pestaña **Detalles** , haga clic en **Guardar**. Aparece el cuadro de diálogo **Guardar como** . Localice la carpeta en la que desee guardar la configuración de registro, escriba un nombre de archivo para la nueva configuración de registro y haga clic en **Guardar**.  
  
10. Haga clic en **OK**.  
  
11. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Integration Services &#40;SSIS&#41; registro](performance/integration-services-ssis-logging.md)   
 [Registro de Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
