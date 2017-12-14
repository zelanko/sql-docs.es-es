---
title: Administrador de escalabilidad horizontal de SQL Server Integration Services | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84fe58d4dc7894728c43cb19d17d3444b5b84820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-scale-out-manager"></a>Administrador de escalabilidad horizontal de Integration Services

El administrador de escalabilidad horizontal es una herramienta de administración que le permite gestionar la topología completa de la escalabilidad horizontal de SSIS en una única ubicación. Elimina la necesidad de operar en varias máquinas y tener que trabajar con comandos TSQL. 

Existen dos formas de desencadenar el administrador de escalabilidad horizontal.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Abrir el administrador de escalabilidad horizontal desde SQL Server Management Studio
Abra SQL Server Management Studio y conéctese a la instancia de SQL Server del patrón de escalabilidad horizontal.

Haga clic con el botón derecho en **SSISDB** en el Explorador de objetos y seleccione **Administrar escalabilidad horizontal...**. ![Administrar escalabilidad horizontal](media/manage-scale-out.PNG)

> [!NOTE]
> Se recomienda ejecutar SQL Server Management Studio como administrador, ya que algunas de las operaciones de administración de escalabilidad horizontal, como "Agregar un trabajo de escalabilidad horizontal", requerirán privilegios administrativos.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. Abrir el administrador de escalabilidad horizontal ejecutando directamente ISManager.exe

Podrá encontrar el archivo ISManager.exe en %SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management. Haga clic con el botón derecho en **ISManager.exe** y seleccione "Ejecutar como administrador". 

Una vez abierto, debe especificar el nombre de SQL Server del patrón de escalabilidad horizontal y conectarse a él antes de administrar la escalabilidad horizontal.

![Conexión del portal](media/portal-connect.PNG)

El administrador de escalabilidad horizontal proporciona varias funcionalidades que se indican a continuación. 

## <a name="enable-scale-out"></a>Habilitar la escalabilidad horizontal
Después de conectarse a SQL Server, si la escalabilidad horizontal no está habilitada, puede hacer clic en el botón "Habilitar" para habilitarla.

![Habilitar la escalabilidad horizontal en el portal](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Ver el estado del patrón de escalabilidad horizontal
El estado del patrón de escalabilidad horizontal se muestra en la página **Panel**.

![Panel del portal](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Ver el estado del trabajo de escalabilidad horizontal
El estado del trabajo de escalabilidad horizontal se muestra en la página **Administrador del trabajo**. Puede hacer clic en cada trabajo para ver cada estado de forma individual.

![Administrador del trabajo del portal](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Agregar el trabajo de escalabilidad horizontal
Para agregar un trabajo de escalabilidad horizontal, haga clic en el botón "+" en la parte inferior de la lista de trabajos de escalabilidad horizontal. 

Escriba el nombre de máquina del trabajo de escalabilidad horizontal que quiera agregar y haga clic en "Validar". El administrador de escalabilidad horizontal comprobará si el usuario actual tiene acceso a los almacenes de certificados de las máquinas del patrón de escalabilidad horizontal y el trabajo de escalabilidad horizontal.

![Conectar el trabajo](media/connect-worker.PNG)

Si la validación es correcta, el administrador de escalabilidad horizontal intentará leer el archivo de configuración del trabajo y obtener la huella digital del certificado del mismo. Para obtener más información, consulte [Scale Out Worker (Trabajo de escalabilidad horizontal)](integration-services-ssis-scale-out-worker.md). Si no es capaz de leer el archivo de configuración del trabajo, existen dos alternativas que puede usar para proporcionar el certificado de trabajo. 

Puede introducir directamente la huella digital del certificado de trabajo 

![Certificado de trabajo 1](media/portal-cert1.PNG)

o proporcionar el archivo del certificado. 

![Certificado de trabajo 2](media/portal-cert2.PNG)

Después de recopilar toda la información, el administrador de escalabilidad horizontal le indicará qué acciones debe realizar. Normalmente se incluye la instalación del certificado, la actualización del archivo de configuración del trabajo y el proceso de reinicio del servicio de trabajo. 

![Agregar confirmación 1 en el portal](media/portal-add-confirm1.PNG)

En caso de que el certificado de trabajo no sea accesible, debe actualizarlo manualmente y reiniciar el servicio de trabajo.

![Agregar confirmación 2 en el portal](media/portal-add-confirm2.PNG)

Haga clic en la casilla "Confirmar" y comience a agregar el trabajo de escalabilidad horizontal.

## <a name="delete-scale-out-worker"></a>Eliminar el trabajo de escalabilidad horizontal
Para eliminar un trabajo de escalabilidad horizontal, selecciónelo y haga clic en el botón "-" situado en la parte inferior de la lista del trabajo en cuestión.


## <a name="enabledisable-scale-out"></a>Habilitar o deshabilitar la escalabilidad horizontal
Para habilitar o deshabilitar un trabajo de escalabilidad horizontal, selecciónelo y haga clic en el botón "Habilitar trabajo" o "Deshabilitar trabajo". El estado del trabajo del administrador de escalabilidad horizontal cambiará según lo establecido, siempre y cuando el trabajo no esté desconectado.

## <a name="edit-scale-out-worker-description"></a>Editar la descripción del trabajo de escalabilidad horizontal
Para editar la descripción de un trabajo de escalabilidad horizontal, seleccione el trabajo en cuestión y haga clic en el botón "Editar". Cuando termine de editar, haga clic en el botón "Guardar".

![Guardar el trabajo en el portal](media/portal-save-worker.PNG)

