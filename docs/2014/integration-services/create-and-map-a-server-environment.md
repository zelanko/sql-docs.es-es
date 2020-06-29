---
title: Crear y asignar un entorno de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isenvprop.variables.f1
- sql12.ssis.ssms.iscreateenv.f1
- sql12.ssis.ssms.isenvprop.permissions.f1
- sql12.ssis.ssms.isenvprop.general.f1
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 02fecbe0a98770a116a0ae2558dc354ddae24755
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437882"
---
# <a name="create-and-map-a-server-environment"></a>Crear y asignar un entorno de servidor
  Los entornos de servidor se crean con el fin de especificar valores en tiempo de ejecución para los paquetes contenidos en un proyecto implementado en el servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Después puede asignar las variables de entorno a parámetros para un paquete concreto, para los paquetes de punto de entrada o para todos los paquetes de un proyecto determinado. Un paquete de punto de entrada suele ser un paquete primario que ejecuta un paquete secundario.  
  
> [!IMPORTANT]  
>  Para una ejecución determinada, un paquete solo puede ejecutarse con los valores contenidos en un único entorno de servidor.  
  
 Puede consultar las vistas para obtener una lista de entornos de servidor, referencias de entorno y variables de entorno. También puede llamar a procedimientos almacenados para agregar, eliminar y modificar entornos, referencias de entorno y variables de entorno. Para obtener más información, vea la sección **Entornos de servidor, variables de servidor y referencias del entorno de servidor** en [SSIS Catalog](catalog/ssis-catalog.md).  
  
### <a name="to-create-and-use-a-server-environment"></a>Para crear y utilizar un entorno de servidor  
  
1.  En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] , expanda el [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nodo catálogos> **SSISDB** en explorador de objetos y busque la carpeta **entornos** del proyecto para el que desea crear un entorno.  
  
2.  Haga clic con el botón derecho en la carpeta **Entornos** y, después, haga clic en **Crear entorno**.  
  
3.  Escriba un nombre para el entorno y opcionalmente una descripción y, a continuación, haga clic en **Aceptar**.  
  
4.  Haga clic con el botón derecho en el nuevo entorno y, después, haga clic en **Propiedades**.  
  
5.  En la página **Variables** , haga lo siguiente para agregar una variable.  
  
    1.  Seleccione **Tipo** para la variable. **No** es necesario que el nombre de la variable coincida con el nombre del parámetro del proyecto al que asignará la variable.  
  
    2.  Escriba la **Descripción** opcional para la variable.  
  
    3.  Escriba el **Valor** para la variable de entorno.  
  
         Para obtener información sobre las reglas para los nombres de las variables de entorno, vea la sección **Variable de entorno** en [SSIS Catalog](catalog/ssis-catalog.md).  
  
    4.  Indique si la variable contiene un valor confidencial; para ello, active o desactive la casilla **Confidencial** .  
  
         Si selecciona **Confidencial**, el valor de la variable no aparece en el campo **Valor** .  
  
         Los valores confidenciales se cifran en el catálogo de SSISDB. Para obtener más información acerca del cifrado, vea [SSIS Catalog](catalog/ssis-catalog.md).  
  
6.  En la página **Permisos** , haga lo siguiente para conceder o denegar permisos para los usuarios y roles seleccionados.  
  
    1.  Haga clic en **Examinar**y, a continuación, seleccione uno o más usuarios y roles en el cuadro de diálogo **Examinar todas las entidades** .  
  
    2.  En el área **Inicios de sesión o roles** , seleccione el usuario o el rol al que desea conceder o denegar permisos.  
  
    3.  En el área **Explícito** , haga clic en **Conceder** o **Denegar** junto a cada permiso.  
  
7.  Para incluir el entorno en el script, haga clic en **Script**. De forma predeterminada, el script aparece en una nueva ventana del Editor de consultas.  
  
    > [!TIP]  
    >  Tiene que hacer clic en **Script** después de realizar cambios en las propiedades del entorno (como agregar una variable) y antes de hacer clic en **Aceptar** en el cuadro de diálogo **Propiedades del entorno**. De lo contrario, no se generará un script.  
  
8.  Haga clic en **Aceptar** para guardar los cambios realizados en las propiedades de entorno.  
  
9. En el nodo **SSISDB** del Explorador de objetos, expanda la carpeta **Proyectos** , haga clic con el botón derecho en el proyecto y, después, haga clic en **Configurar**.  
  
10. En la página **Referencias** , haga clic en **Agregar** para agregar un entorno y, a continuación, haga clic en **Aceptar** para guardar la referencia al entorno.  
  
11. Vuelva a hacer clic con el botón derecho en el proyecto y, después, haga clic en **Configurar**.  
  
12. Para asignar la variable de entorno a un parámetro que agregó al paquete en tiempo de diseño o a un parámetro que se generó cuando convirtió el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al modelo de implementación del proyecto, haga lo siguiente.  
  
    1.  En la pestaña **Parámetros** de la página **Parámetros** , haga clic en el botón Examinar situado junto al campo **Valor** .  
  
    2.  Haga clic en **Usar variable de entorno**y seleccione la variable de entorno que creó.  
  
13. Para asignar la variable de entorno a una propiedad del administrador de conexiones, haga lo siguiente. Se generan automáticamente parámetros en el servidor SSIS para las propiedades del administrador de conexiones.  
  
    1.  En la pestaña **Administradores de conexiones** de la página **Parámetros** , haga clic en el botón Examinar situado junto al campo **Valor** .  
  
    2.  Haga clic en **Usar variable de entorno**y seleccione la variable de entorno que creó.  
  
14. Haga clic en **Aceptar** dos veces para guardar los cambios.  
  
  
