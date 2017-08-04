---
title: Escalar horizontalmente el Administrador de SQL Server Integration Services | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96748296acd1b2f5ba98558335fece9637eadb87
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-scale-out-manager"></a>Integration Services escalada Manager

Escala Out Manager es una herramienta de administración que le permite administrar la topología de SSIS horizontalmente completa en una única ubicación. Elimina la carga de operar en varios equipos y trabajar con comandos TSQL. 

Hay dos formas de activar el Administrador de salida de escala.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Abra el escalado horizontal Manager desde SQL Server Management Studio
Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de escala Out Master.

Haga clic en **SSISDB** en el Explorador de objetos y seleccione **administrar horizontalmente...** . 
![Administrar el escalado horizontal](media/manage-scale-out.PNG)

> [!NOTE]
> Se recomienda ejecutar SQL Server Management Studio como administrador como algunas de las operaciones de administración horizontalmente como "Agregar un trabajo de ampliación" requerirá privilegios administrativos.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. Abrir Administrador de fuera de escala, que ejecutan ISManager.exe directamente

ISManager.exe busca en %SystemDrive%\Program archivos (x86) \Microsoft SQL Server\140\DTS\Binn\Management. Haga clic en **ISManager.exe** y seleccione "Ejecutar como administrador". 

Una vez que se abre, debe especificar el nombre de Sql Server del maestro fuera de la escala y conectarse a ella antes de administrar su horizontalmente.

![Conexión del portal](media/portal-connect.PNG)

Escala Out Manager proporciona funcionalidades como sigue. 

## <a name="enable-scale-out"></a>Habilitar el escalado horizontal
Después de conectarse a SQL Server, si no está habilitado horizontalmente, puede hacer clic en el botón "Habilitar" para habilitarlo.

![Habilitar portal escalada](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Ver el estado de escala Out Master
El estado de escala Out Master se muestra en el **panel** página.

![Panel del portal](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Ver el estado de escala Out trabajo
El estado de escala Out trabajo se muestra en el **director trabajador** página. Puede hacer clic en cada proceso de trabajo para ver el estado individual.

![Portal de administrador de trabajo](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Agregar escalada de trabajo
Para agregar un trabajo de salida de escala, haga clic en el botón "+" en la parte inferior de la lista de escala a un trabajador. 

Escriba el nombre de máquina de la escala fuera trabajo que desea agregar y haga clic en "Validar". La escala fuera Manager comprobará si el usuario actual tiene acceso a los almacenes de certificados en las máquinas de escala Out maestra y de escala Out trabajo.

![Conectar el trabajo](media/connect-worker.PNG)

Si la validación es correcta, escala Out Manager intentará leer el archivo de configuración de su trabajo y obtener la huella digital del certificado del trabajador. Para obtener más información, consulte [escala Out trabajo](integration-services-ssis-scale-out-worker.md). Si no es capaz de leer al trabajo en el archivo de configuración, hay dos formas alternativas para proporcionar el certificado de trabajo. 

O bien puede escribir directamente la huella digital del certificado de trabajo 

![Certificado del trabajo 1](media/portal-cert1.PNG)

o bien, proporcione el archivo de certificado. 

![Certificado del trabajo 2](media/portal-cert2.PNG)

Después de recopilar toda la información, escalado Out administrador le proporcionará las acciones que debe realizar. Tyically, incluye el reinicio del servicio de trabajo, actualización del archivo de configuración de trabajo e instalación de certificados. 

![Portal de agregar confirmar 1](media/portal-add-confirm1.PNG)

En caso de que el certificado de trabajo no está accesible, debe actualizarlo manualmente por usted mismo y reinicie el servicio de trabajo.

![Portal de agregar confirmar 2](media/portal-add-confirm2.PNG)

Haga clic en la casilla de verificación Confirmar y empezar a agregar escala Out trabajo.

## <a name="delete-scale-out-worker"></a>Eliminar escalada de trabajo
Para eliminar un trabajo de salida de escala, seleccione el trabajo de salida de escala y haga clic en el "-" situado en la parte inferior de la lista de escala a trabajadores.


## <a name="enabledisable-scale-out"></a>Habilitar o deshabilitar escalado horizontal
Para habilitar o deshabilitar a un trabajo de salida de escala, seleccione el trabajo de salida de escala y haga clic en el botón de "Deshabilitar trabajo" o "Habilitar trabajo". El estado de trabajo en escala Out administrador cambiará en consecuencia si el trabajo no está sin conexión.

## <a name="edit-scale-out-worker-description"></a>Editar descripción de escala Out trabajo
Para editar la descripción de un trabajo de salida de escala, seleccione el trabajo de salida de escala y haga clic en el botón "Edit". Cuando termine de editar, haga clic en el botón "Guardar".

![Portal de guardar el trabajo](media/portal-save-worker.PNG)


