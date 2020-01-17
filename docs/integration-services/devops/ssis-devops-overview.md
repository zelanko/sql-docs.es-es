---
title: Introducción a SQL Server Integration Services DevOps | Microsoft Docs
description: Aprenda a crear CICD en SSIS con las herramientas de DevOps de SSIS.
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 11ed5aa2ddcd675d201fc86abf595055828d7621
ms.sourcegitcommit: 3511da65d7ebc788e04500bbef3a3b4a4aeeb027
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/06/2020
ms.locfileid: "75681776"
---
# <a name="sql-server-integration-services-ssis-devops-tools-preview"></a>Herramientas de DevOps para SQL Server Integration Services (versión preliminar)

La extensión [SSIS DevOps Tools](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) está disponible en el **marketplace de Azure DevOps**.

Si no dispone de ninguna organización de **Azure DevOps**, primero debe registrarse en [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops) y, después, agregar la extensión **SSIS DevOps Tools** siguiendo [estos pasos](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension).

Las **herramientas de DevOps de SSIS** incluyen la tarea **de compilación de SSIS** y la tarea de la versión **de implementación de SSIS**.

- La tarea **de compilación de SSIS** admite la generación de archivos dtproj en el modelo de implementación de proyectos o en el modelo de implementación de paquetes.

- La tarea **de implementación de SSIS** admite la implementación de archivos ISPAC individuales o múltiples en el catálogo de SSIS local y en Azure-SSIS IR, o de archivos SSISDeploymentManifest y sus archivos asociados en un recurso compartido de archivos locales o de Azure.

## <a name="ssis-build-task"></a>Tarea de compilación de SSIS

![tarea de compilación](media/ssis-build-task.png)

### <a name="properties"></a>Propiedades

#### <a name="project-path"></a>Ruta de acceso del proyecto

Ruta de acceso de la carpeta o el archivo del proyecto que se va a compilar. Si se especifica una ruta de acceso de carpeta, la tarea de compilación de SSIS buscará todos los archivos dtproj de forma recursiva en esta carpeta y los compilará todos.

#### <a name="project-configuration"></a>Configuración de proyecto

Nombre de la configuración del proyecto que se va a usar para la compilación. Si no se proporciona, el valor predeterminado es la primera configuración de proyecto definida en cada archivo dtproj.

#### <a name="output-path"></a>Ruta de acceso de resultados

Ruta de acceso de una carpeta independiente para guardar los resultados de la compilación, que se pueden publicar como artefactos de compilación a través de una [tarea de publicación de artefactos de compilación](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops).

### <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

- La tarea de compilación de SSIS se basa en Visual Studio y en el diseñador de SSIS, que es obligatorio en los agentes de compilación. Por lo tanto, para ejecutar la tarea de compilación de SSIS en la canalización, debe elegir **vs2017-win2016** para los agentes hospedados en Microsoft o bien instalar Visual Studio y el diseñador de SSIS (ya sea VS2017 + SSDT2017 o VS2019 + la extensión de proyectos de SSIS) en agentes autohospedados.

- Para compilar proyectos de SSIS mediante el uso de componentes integrados (incluido Azure Feature Pack de SSIS y otros componentes de terceros), los componentes integrados deben instalarse en el equipo en el que se ejecuta el agente de canalización.  Para el agente hospedado por Microsoft, el usuario puede agregar una [tarea PowerShell Script](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops) o una [Command Line Script](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops) para descargar e instalar los componentes antes de que se ejecute la tarea de compilación de SSIS.

- En la tarea de compilación de SSIS no se admiten los niveles de protección **EncryptSensitiveWithPassword** y **EncryptAllWithPassword**. Asegúrese de que todos los proyectos de SSIS del código base no usan ninguno de estos dos niveles de protección para evitar que la tarea de compilación de SSIS se bloquee y agote el tiempo de espera durante la ejecución.

## <a name="ssis-deploy-task"></a>Tarea de implementación de SSIS

![tarea de implementación](media/ssis-deploy-task.png)

### <a name="properties"></a>Propiedades

#### <a name="source-path"></a>Ruta de origen

Ruta de acceso de los archivos de origen ISPAC o SSISDeploymentManifest que quiere implementar. Esta ruta de acceso puede ser una ruta de acceso a una carpeta o a un archivo.

#### <a name="destination-type"></a>Tipo de destino

Tipo de destino. Actualmente, la tarea de implementación de SSIS admite dos tipos de destino:

- *Sistema de archivos*: los archivos SSISDeploymentManifest y sus archivos asociados se implementan en un sistema de archivos especificado. Se admiten recursos compartidos de archivos tanto locales como en Azure.
- *SSISDB*: los archivos ISPAC se implementan en un catálogo de SSIS específico, que se puede hospedar localmente en SQL Server o en Azure-SSIS Integration Runtime.

#### <a name="destination-server"></a>Servidor de destino

Nombre del servidor de SQL de destino. Puede ser el nombre de una instancia administrada de SQL Server, Azure SQL Database o Azure SQL Database local. Esta propiedad solo es visible cuando el tipo de destino es SSISDB.

#### <a name="destination-path"></a>Ruta de acceso de destino

Ruta de acceso de la carpeta de destino en la que se implementará el archivo de código fuente. Por ejemplo:

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

La tarea de implementación de SSIS creará la carpeta y la subcarpeta, si no existen.

#### <a name="authentication-type"></a>Tipo de autenticación

Tipo de autenticación para acceder al servidor de destino especificado. Esta propiedad solo es visible cuando el tipo de destino es SSISDB. En general, la tarea de implementación de SSIS admite cuatro tipos de autenticación:

- Autenticación de Windows
- Autenticación de SQL Server
- Active Directory - Contraseña
- Active Directory - Integrado

Pero el hecho de que se admita un tipo de autenticación determinado depende del tipo de servidor y del tipo de agente de destino. En la tabla siguiente se muestra la matriz de compatibilidad detallada.

| |Agente hospedado por Microsoft|Agente autohospedado|
|---------|---------|---------|
|SQL Server local o máquina virtual |N/D|Autenticación de Windows|
|Azure SQL|Autenticación de SQL Server <br> Active Directory - Contraseña|Autenticación de SQL Server <br> Active Directory - Contraseña <br> Active Directory - Integrado|

#### <a name="domain-name"></a>Nombre de dominio

Nombre de dominio para acceder al sistema de archivos especificado. Esta propiedad solo es visible cuando el tipo de destino es Sistema de archivos.
Puede dejarla vacía cuando la cuenta de usuario que va a ejecutar el agente autohospedado haya obtenido acceso de lectura/escritura a la ruta de acceso al destino especificado.

#### <a name="username"></a>Nombre de usuario

Nombre de usuario para acceder al sistema de archivos especificado o a SSISDB. Esta propiedad está visible cuando el tipo de destino es el sistema de archivos o el tipo de autenticación es Autenticación de SQL Server o Active Directory - Contraseña.
Puede dejarla vacía cuando el tipo de destino sea el sistema de archivos y la cuenta de usuario que va a ejecutar el agente autohospedado haya obtenido acceso de lectura/escritura a la ruta de acceso al destino especificado.

#### <a name="password"></a>Contraseña

Contraseña para acceder al sistema de archivos especificado o a SSISDB. Esta propiedad está visible cuando el tipo de destino es el sistema de archivos o el tipo de autenticación es Autenticación de SQL Server o Active Directory - Contraseña.
Puede dejarla vacía cuando el tipo de destino sea el sistema de archivos y la cuenta de usuario que va a ejecutar el agente autohospedado haya obtenido acceso de lectura/escritura a la ruta de acceso al destino especificado.

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>Sobreescritura de proyectos existentes o archivos SSISDeploymentManifest con los mismos nombres

Especifica si se sobrescriben los proyectos existentes o archivos SSISDeploymentManifest con los mismos nombres. En caso negativo, la tarea de implementación de SSIS omite la implementación de esos proyectos o archivos.

#### <a name="continue-deployment-when-error-occurs"></a>Implementación continua al producirse un error

Especifica si TP continúa con la implementación de los proyectos o archivos restantes cuando se produce un error. En caso negativo, la tarea de implementación de SSIS se detiene inmediatamente cuando se produce un error.

### <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

En estos momentos, la tarea de implementación de SSIS no admite los siguientes escenarios:

- Configuración del entorno en el catálogo de SSIS.
- Implemente ISPAC en Azure SQL Server o en la instancia administrada de Azure SQL, ya que solo admite la autenticación multifactor (MFA).
- Implementación de paquetes en MSDB o en el almacén de paquetes de SSIS.

## <a name="release-notes"></a>Notas de la versión

### <a name="version-011-preview"></a>Versión 0.1.1 (versión preliminar)

Fecha de lanzamiento: 6 de enero de 2020

- Se ha agregado una restricción del requisito de versión mínima del agente. Actualmente, la versión mínima del agente de este producto es 2.144.0.
- Se han corregido algunos textos de visualización incorrectos para la tarea de implementación de SSIS.
- Se han modificado algunos mensajes de error.

### <a name="version-010-preview"></a>Versión 0.1.0 (versión preliminar)

Fecha de lanzamiento: 5 de diciembre de 2019

Versión inicial de las herramientas de DevOps para SSIS. Se trata de una versión preliminar.

## <a name="next-steps"></a>Pasos siguientes

- Obtener la [extensión SSIS DevOps](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)
