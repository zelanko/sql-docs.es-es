---
title: Instalar Distributed Replay utilizando un archivo de configuración | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
caps.latest.revision: 14
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4167456a5d1b59dd44451dda26f3ccb56e417a56
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155696"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>Instalar Distributed Replay utilizando un archivo de configuración
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite generar un archivo de configuración basado en la entrada de usuario y en la configuración predeterminada del sistema. Si especifica que desea que se instalen las herramientas de administración, puede utilizar el archivo de configuración para implementar los tres componentes de Distributed Replay (herramienta de administración, controlador de Distributed Replay y cliente Distributed Replay). Admite la instalación, reparación y desinstalación de los componentes de Distributed Replay.  
  
 El programa de instalación admite el uso del archivo de configuración solamente a través de la línea de comandos. A continuación se indica el orden de procesamiento de los parámetros cuando se usa el archivo de configuración:  
  
-   El archivo de configuración sobrescribe los valores predeterminados de un paquete.  
  
-   Los valores de línea de comandos sobrescriben los valores del archivo de configuración.  
  
 Para obtener más información sobre cómo usar un archivo de configuración, consulte [instalar SQL Server 2014 mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md).  
  
> [!IMPORTANT]  
>  Después de instalar Distributed Replay, debe crear las reglas de firewall en los equipos cliente y de controlador, y conceder a cada equipo cliente permisos en el servidor de destino. Para obtener más información, vea [Completar los pasos posteriores a la instalación](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
### <a name="to-generate-a-configuration-file"></a>Para generar un archivo de configuración  
  
1.  Siga los pasos del asistente para instalación hasta llegar a la página **Listo para instalar** . La ruta de acceso al archivo de configuración se especifica en la sección que así lo indica en la página **Listo para instalar** .  
  
2.  Cancele la instalación sin completarla realmente para generar el archivo INI.  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>Para instalar Distributed Replay utilizando el archivo de configuración  
  
-   Realice la instalación utilizando el símbolo del sistema y proporcione el archivo ConfigurationFile.ini mediante el parámetro ConfigurationFile.  
  
 **Sintaxis de ejemplo**  
  
 A continuación figura un ejemplo sobre cómo especificar el archivo de configuración en el símbolo del sistema:  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  Debe especificar ambas contraseñas en la línea de comandos porque no puede configurarlas en el archivo de configuración.  
  
  
