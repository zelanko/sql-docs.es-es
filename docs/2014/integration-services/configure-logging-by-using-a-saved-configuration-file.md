---
title: Configurar el registro mediante un archivo de configuración guardado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- logs [Integration Services], containers
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bf4bea14cafe771f4fe20e640601ea37adfe97fc
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921608"
---
# <a name="configure-logging-by-using-a-saved-configuration-file"></a>Configurar el registro utilizando un archivo de configuración guardado
  Este procedimiento describe cómo configurar el registro para los contenedores nuevos de un paquete, cargando un archivo de configuración de registro previamente guardado.  
  
 De manera predeterminada, todos los contenedores de un paquete utilizan la misma configuración de registro que el contenedor principal. Por ejemplo, las tareas de un bucle ForEach utilizan la misma configuración de registro que el bucle ForEach.  
  
### <a name="to-configure-logging-for-a-container"></a>Para configurar el registro para un contenedor  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el menú **SSIS** , haga clic en **Registro**.  
  
3.  Expanda la vista de árbol del paquete y seleccione el contenedor que desee configurar.  
  
4.  En la pestaña **Proveedores y registros** , seleccione los registros que desee utilizar para el contenedor.  
  
    > [!NOTE]  
    >  Solo puede crear registros en el nivel de paquete. Para más información, vea [Habilitar el registro de paquetes en SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md).  
  
5.  Haga clic en la pestaña **Detalles** y, a continuación, en **Cargar**.  
  
6.  Localice el archivo de configuración del registro que desee utilizar y haga clic en **Abrir**.  
  
7.  También puede seleccionar una entrada diferente del registro al activar la casilla correspondiente en la columna **Eventos** . Haga clic en **Avanzadas** para seleccionar el tipo de información que se debe registrar para esta entrada.  
  
    > [!NOTE]  
    >  El nuevo contenedor puede incluir entradas de registro adicionales que no estén disponibles para el contenedor utilizado originalmente para crear la configuración del registro. Es necesario seleccionar manualmente estas entradas adicionales para que se registren.  
  
8.  Para guardar la versión actualizada de la configuración de registro, haga clic en **Guardar**.  
  
9. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Registro de Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
