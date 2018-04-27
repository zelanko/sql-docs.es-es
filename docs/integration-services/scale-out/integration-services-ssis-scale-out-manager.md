---
title: Administrador de escalabilidad horizontal de SQL Server Integration Services | Microsoft Docs
ms.description: This article describes the Scale Out Manager tool which you can use to manager SSIS Scale Out
ms.custom: ''
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e7d9120273330d4beab9e859fa17dde4caa0b04
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-scale-out-manager"></a>Administrador de escalabilidad horizontal de Integration Services

El administrador de escalabilidad horizontal es una herramienta que permite administrar toda la topología de escalabilidad horizontal de SSIS desde una sola aplicación. De este modo, es posible evitar tener que realizar las tareas de administración y ejecutar los comandos Transact-SQL en varios equipos.

## <a name="open-scale-out-manager"></a>Abrir el Administrador de escalabilidad horizontal

Hay dos maneras de abrir el Administrador de escalabilidad horizontal.

### <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Abrir el administrador de escalabilidad horizontal desde SQL Server Management Studio
Abra SQL Server Management Studio (SSMS) y conéctese a la instancia de SQL Server del Administrador de escalabilidad horizontal.

En el Explorador de objetos, haga clic con el botón derecho en **SSISDB** y seleccione **Administrar escalabilidad horizontal**.

![Administrar escalabilidad horizontal](media/manage-scale-out.PNG)

> [!NOTE]
> Se recomienda ejecutar SSMS como administrador, ya que algunas de las operaciones de administración de la escalabilidad horizontal, como agregar un trabajo de escalabilidad horizontal, requieren privilegios administrativos.

### <a name="2-open-scale-out-manager-by-running-ismanagerexe"></a>2. Abrir el Administrador de escalabilidad horizontal ejecutando ISManager.exe

Busque `ISManager.exe` en `%SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management`. Haga clic con el botón derecho en **ISManager.exe** y seleccione **Ejecutar como administrador**. 

Cuando se abra, escriba el nombre de la instancia de SQL Server del Servicio principal de escalabilidad horizontal y conéctese para administrar el entorno de escalabilidad horizontal.

![Conexión del portal](media/portal-connect.PNG)

## <a name="tasks-available-in-scale-out-manager"></a>Tareas disponibles en el Administrador de escalabilidad horizontal
En el Administrador de escalabilidad horizontal, puede hacer lo siguiente:

### <a name="enable-scale-out"></a>Habilitar la escalabilidad horizontal
Después de conectarse a SQL Server, si la escalabilidad horizontal no está habilitada, puede hacer clic en **Habilitar**.

![Habilitar la escalabilidad horizontal en el portal](media/portal-enable-scale-out.PNG) 

### <a name="view-scale-out-master-status"></a>Ver el estado del patrón de escalabilidad horizontal
El estado del patrón de escalabilidad horizontal se muestra en la página **Panel**.

![Panel del portal](media/portal-dashboard.PNG)

### <a name="view-scale-out-worker-status"></a>Ver el estado del trabajo de escalabilidad horizontal
El estado del trabajo de escalabilidad horizontal se muestra en la página **Administrador del trabajo**. Puede seleccionar cada trabajo para ver su estado de forma individual.

![Administrador del trabajo del portal](media/portal-worker-manager.PNG)

### <a name="add-a-scale-out-worker"></a>Agregar un trabajo de escalabilidad horizontal
Para agregar un trabajo de escalabilidad horizontal, haga clic en **+**, en la parte inferior de la lista de trabajos de escalabilidad horizontal. 

Escriba el nombre del equipo del trabajo de escalabilidad horizontal que quiera agregar y haga clic en **Validar**. El Administrador de escalabilidad horizontal comprobará si el usuario actual tiene acceso a los almacenes de certificados del Servicio principal de escalabilidad horizontal y a los equipos de trabajo de escalabilidad horizontal.

![Conectar el trabajo](media/connect-worker.PNG)

Si la validación es correcta, el Administrador de escalabilidad horizontal intentará leer el archivo de configuración del servidor del trabajo y obtener la huella digital del certificado de este. Para obtener más información, vea [Trabajo de escalabilidad horizontal](integration-services-ssis-scale-out-worker.md). Si no es capaz de leer el archivo de configuración del trabajo, existen dos alternativas que puede utilizar para proporcionar el certificado de trabajo. 

1.  Puede especificar directamente la huella digital del certificado de trabajo.

    ![Certificado de trabajo 1](media/portal-cert1.PNG)

2.  O bien, puede proporcionar el archivo del certificado. 

    ![Certificado de trabajo 2](media/portal-cert2.PNG)

Después de recopilar toda la información, el Administrador de escalabilidad horizontal le indicará qué acciones debe realizar. Normalmente, estas acciones incluyen la instalación del certificado, la actualización del archivo de configuración de servicio del trabajo y el reinicio del servicio del trabajo.

![Agregar confirmación 1 en el portal](media/portal-add-confirm1.PNG)

En caso de que no se pueda acceder al certificado del trabajo, deberá actualizarlo manualmente y reiniciar el servicio del trabajo.

![Agregar confirmación 2 en el portal](media/portal-add-confirm2.PNG)

Active la casilla **Confirmar** y, a continuación, haga clic en **Aceptar** para empezar a agregar un trabajo de escalabilidad horizontal.

### <a name="delete-a-scale-out-worker"></a>Eliminación del trabajo de escalabilidad horizontal
Para eliminar un trabajo de escalabilidad horizontal, selecciónelo y haga clic en **-**, en la parte inferior de la lista del trabajo en cuestión.

### <a name="enable-or-disable-a-scale-out-worker"></a>Habilitar o deshabilitar un trabajo de escalabilidad horizontal
Para habilitar o deshabilitar un trabajo de escalabilidad horizontal, selecciónelo y haga clic en **Habilitar trabajo** o **Deshabilitar trabajo**. Si el trabajo dispone de conexión, el estado del trabajo que aparece en el Administrador de escalabilidad horizontal cambiará según corresponda.

## <a name="edit-a-scale-out-worker-description"></a>Editar la descripción de un trabajo de escalabilidad horizontal
Para editar la descripción de un trabajo de escalabilidad horizontal, seleccione el trabajo en cuestión y haga clic en **Editar**. Cuando termine de editar la descripción, haga clic en **Guardar**.

![Guardar el trabajo en el portal](media/portal-save-worker.PNG)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea los artículos siguientes:
-   [Servicio principal de escalabilidad horizontal de Integration Services (SSIS)](integration-services-ssis-scale-out-master.md)
-   [Trabajo de escalabilidad horizontal de Integration Services (SSIS)](integration-services-ssis-scale-out-worker.md)