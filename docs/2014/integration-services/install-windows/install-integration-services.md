---
title: Instalar Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7cc7cb929aa34c9226dbdff9efb6b0c918b546f1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425062"
---
# <a name="install-integration-services"></a>Instalar Integration Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único programa de instalación para instalar alguno de sus componentes o todos, incluido [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Mediante el programa de instalación puede instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con o sin otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un único equipo.  
  
 En este tema se destacan consideraciones importantes que se deberían conocer antes de instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. La información de este tema le ayudará a evaluar las opciones de instalación para que pueda realizar selecciones que deriven en una instalación correcta.  
  
 En este tema no se incluyen instrucciones para iniciar el programa de instalación, usar el Asistente para la instalación o ejecutarlo desde la línea de comandos. Para obtener instrucciones paso a paso sobre cómo iniciar el programa de instalación y seleccionar los componentes que se van a instalar, consulte [instalación de inicio rápido de SQL Server 2014](../../getting-started/quick-start-installation-of-sql-server-2014.md). Para obtener información acerca de las opciones de la línea de comandos para instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Install SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="preparing-to-install-integration-services"></a>Preparar la instalación de Integration Services  
 Antes de instalar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , revise los siguientes requisitos:  
  
-   [Requisitos de hardware y software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Comprobar los parámetros del Comprobador de configuración del sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)  
  
-   [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
## <a name="selecting-an-integration-services-configuration"></a>Seleccionar una configuración de Integration Services  
 Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en las configuraciones siguientes:  
  
-   Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo que no tenga ninguna instancia anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Puede instalar [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en paralelo con una instancia existente de [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] y [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Al actualizar a [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en un equipo que ya tenga instalada una de estas versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] se instala en paralelo con la versión anterior.  
  
     Para obtener más información sobre cómo actualizar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Actualizar Integration Services](upgrade-integration-services.md). Para obtener más información sobre la compatibilidad con las versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Compatibilidad con versiones anteriores de Integration Services](../integration-services-backward-compatibility.md).  
  
## <a name="installing-integration-services"></a>instalar Integration Services  
 Después de revisar los requisitos de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y asegurarse de que el equipo los cumple, puede comenzar a instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
> [!NOTE]  
>  En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cuando se instalaba [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todos los usuarios del grupo Usuarios tenía acceso al servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de forma predeterminada. Cuando instala [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los usuarios no tienen acceso al servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El servicio es seguro de forma predeterminada. Una vez [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador debe ejecutar la herramienta de configuración de DCOM (Dcomcnfg.exe) para conceder a los usuarios específicos acceso a **SQL Server Integration Services 12,0**.  
>   
>  Para obtener instrucciones acerca de cómo conceder permisos, vea [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md).  
  
 Si está usando el Asistente para la instalación con el fin de instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usará una serie de páginas para especificar los componentes y las opciones. A continuación se muestran páginas del Asistente para la instalación en las que las opciones que seleccione afectan a la instalación de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con recomendaciones de selección:  
  
-   **Selección de características**  
  
     Seleccione **Integration Services** para instalar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y ejecutar paquetes fuera del entorno de diseño.  
  
     Para realizar una instalación completa de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], junto con las herramientas y la documentación para desarrollar y administrar paquetes, seleccione **Integration Services** y las **Características compartidas**siguientes:  
  
    -   **SQL Server Data Tools** para instalar las herramientas para diseñar paquetes.  
  
    -   **Herramientas de administración - Completa** para instalar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar paquetes.  
  
    -   **SDK de las herramientas de cliente** para instalar ensamblados administrados para la programación de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Muchas soluciones de almacenamiento de datos también requieren la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes adicionales, como [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Algunos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que puede seleccionar para instalarlos en la página **Selección de características** del Asistente para la instalación instalan un subconjunto parcial de componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Estos componentes resultan útiles para tareas específicas, pero la funcionalidad de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] estará limitada. Por ejemplo, la opción **Servicios de motor de base de datos** instala los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necesarios para el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La opción **Herramientas de datos de SQL Server** instala los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necesarios para diseñar un paquete, pero no se instala el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y no es posible ejecutar paquetes fuera de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Para asegurarse de que la instalación de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]es completa, debe seleccionar **Integration Services** en la página **Selección de características** .  
  
     **Instalación en un equipo de 64 bits** En un equipo de 64 bits, al seleccionar **Integration Services** solo se instala el tiempo de ejecución de 64 bits y las herramientas. Si tiene que ejecutar paquetes en modo de 32 bits, debe seleccionar una opción adicional para instalar el motor de tiempo de ejecución y las herramientas de 32 bits:  
  
    -   Si el equipo de 64 bits está ejecutando el sistema operativo x86, seleccione **SQL Server Data Tools** o **herramientas de administración-completa**.  
  
    -   Si el equipo de 64 bits está ejecutando el [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] sistema operativo, seleccione **herramientas de administración-completa**.  
  
     **Instalar en un servidor dedicado para ETL:** para usar un servidor dedicado para los procesos de extracción, transformación y carga de datos (ETL), recomendamos que instale una instancia local de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] al instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] suele almacenar los paquetes en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y se basa en el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar estos paquetes. Si el servidor ETL no tiene ninguna instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], tendrá que programar o ejecutar los paquetes desde un servidor que sí tenga una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Esto significa que los paquetes no se ejecutarán en el servidor ETL, sino en el servidor desde el que se iniciaron. Como resultado, los recursos del servidor ETL dedicado no se utilizan como se pretendía. Además, los procesos ETL en ejecución pueden agotar los recursos de otros servidores.  
  
-   **Configuración de instancia**  
  
     Cualquier selección que realice en la página **Configuración de instancia** no afecta al [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ni al servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Solo puede instalar una instancia del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo. Se conecta al servicio con el nombre de equipo.  
  
     De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está configurado para administrar los paquetes que están almacenados en la base de datos **msdb** de la instancia del motor de base de datos que se instala al mismo tiempo que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si no se instala al mismo tiempo que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]una instancia del motor de base de datos, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para administrar los paquetes que se almacenan en la base de datos **msdb** de la instancia local predeterminada del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para administrar los paquetes que están almacenados en una instancia con nombre o una instancia remota del [!INCLUDE[ssDE](../../includes/ssde-md.md)], o en varias instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)], tiene que modificar el archivo de configuración. Para obtener más información sobre cómo modificar este archivo de configuración, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../service/integration-services-service-ssis-service.md).  
  
-   **Configuración del servidor**  
  
     Revise la configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en la pestaña **Cuentas de servicio** de la página **Configuración del servidor** .  
  
     Si Windows 7 o Windows Server 2008 R2 está instalado, el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servicio se registra para ejecutarse en la cuenta virtual NT Services\MsDtsServer120 y el **tipo de inicio** es **automático**.  No tiene que escribir una contraseña para la cuenta virtual. Si está instalado Microsoft Vista o Windows Server 2008, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se registra para ejecutarse bajo la cuenta integrada Servicio de red y el **Tipo de inicio** es **Automático**. No tiene que escribir una contraseña para la cuenta Servicio de red integrada.  
  
 De forma predeterminada, en una instalación nueva, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para no registrar en el registro de eventos de aplicación los eventos relacionados con la ejecución de paquetes. Esta configuración impide la generación de demasiadas entradas en el registro de eventos al usar la característica de recopilador de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los eventos que no se registran son EventID 12288, "Se ha iniciado el paquete" y EventID 12289, "El paquete finalizó correctamente". Para registrar estos eventos en el registro de eventos de aplicación, abra el Registro para editarlo. A continuación, en el Registro, busque el nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS y cambie el valor DWORD de la opción LogPackageExecutionToEventLog de 0 a 1.  
  
## <a name="understanding-the-integration-services-service"></a>Descripción del servicio Integration Services  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se instala al seleccionar la opción **Integration Services** en la página **Selección de características** . Al aceptar la configuración predeterminada en la página **Configuración del servidor** , el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se habilita y su **Tipo de inicio** es **Automático**.  
  
 Solo puede instalar una única instancia del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un equipo. El servicio no es específico de una instancia determinada del motor de base de datos. Para realizar la conexión con el servicio, se utiliza el nombre del equipo en el que se ejecuta.  
  
## <a name="installing-integration-services-on-64-bit-computers"></a>Instalar Integration Services en equipos de 64 bits  
  
### <a name="integration-services-features-installed-on-64-bit-computers"></a>Características de Integration Services instaladas en equipos de 64 bits  
 El programa de instalación instala varias características de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] según las opciones de configuración que seleccione:  
  
-   Al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y seleccionar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para la instalación, el programa de instalación instala todas las características y herramientas de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de 64 bits disponibles.  
  
-   Si requiere las características en tiempo de diseño de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , también debe instalar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   Si necesita las versiones de 32 bits de las herramientas y del motor en tiempo de ejecución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para ejecutar ciertos paquetes en modo de 32 bits, también debe instalar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Las características de 64 bits se instalan en el directorio **Archivos de programa** y las de 32 bits se instalan aparte, en el directorio **Archivos de programa (x86)** . (Este comportamiento no es específico de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ni de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el entorno de desarrollo de 32 bits para paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , no se admite en el sistema operativo de 64 bits de [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] y no se instala en los servidores [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] .  
  
  
