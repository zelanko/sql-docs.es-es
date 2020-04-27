---
title: Instalar Distributed Replay (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5b2b43d899041d501039ade4d0493a7fdbf0164
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094630"
---
# <a name="install-distributed-replay-setup"></a>Instalar Distributed Replay (programa de instalación)
  Instalar las características de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay con el Asistente para instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Cuando planee dónde desea instalar las características, tenga en cuenta lo siguiente:  
  
-   Puede instalar la herramienta de administración en el mismo equipo que el controlador de Distributed Replay, o en equipos diferentes.  
  
-   Solo puede haber un controlador en cada entorno de Distributed Replay.  
  
-   Puede instalar el servicio de cliente en 16 equipos (físicos o virtuales) como máximo.  
  
-   Solo una instancia del servicio de cliente se puede instalar en el equipo del controlador de Distributed Replay. Si el entorno de Distributed Replay tiene más de un cliente, no se recomienda instalar el servicio de cliente en el mismo equipo que el controlador. De hacerlo, puede reducirse la velocidad total de la Distributed Replay.  
  
-   En escenarios de pruebas de rendimiento, no se recomienda instalar la herramienta de administración, el servicio Distributed Replay Controller o el servicio de cliente en la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La instalación de todas estas características en el servidor de destino debe limitarse a las pruebas funcionales para la compatibilidad de aplicaciones.  
  
-   Después de la instalación, el servicio de controlador, controlador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, debe ejecutarse antes de iniciarse el servicio de cliente de Distributed Replay en los clientes.  
  
> [!NOTE]  
>  Para quitar o cambiar las características de Distributed Replay, utilice la ventana **Programas y características** de Windows en el **Panel de control**. Seleccione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en la ventana **Desinstalar o cambiar un programa** y, a continuación, haga clic en **Quitar** para abrir el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . En la página **Seleccionar características** , compruebe las características de Distributed Replay que desea quitar.  
  
 **Requisitos previos**  
  
-   Asegúrese de que los equipos que desea utilizar cumplan los requisitos que se describen en el tema [Distributed Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
-   Antes de empezar este procedimiento, cree las cuentas de usuario de dominio en las que se ejecutarán los servicios de controlador y de cliente. Se recomienda que estas cuentas no sean miembros del grupo Administradores de Windows. Para obtener más información, vea la sección sobre cuentas de usuario y de servicio en el tema [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md) .  
  
    > [!NOTE]  
    >  Puede utilizar cuentas de usuario local si está ejecutando la herramienta de administración, el servicio de controlador y el servicio de cliente en el mismo equipo.  
  
 **Ubicaciones de instalación:**  
  
 Suponiendo que utilice las ubicaciones predeterminadas de archivos y una instalación estándar, el directorio base se encuentra en C:\Archivos de programa\Microsoft SQL Server. Dentro de ese directorio, los archivos binarios y los ensamblados se instalan en las siguientes ubicaciones:  
  
-   En un sistema de 32 bits:  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Herramientas  
  
     \- O BIEN -  
  
     \<Directorio de características compartidas\Tools\\(directorio de características compartidas alternativo proporcionado por el usuario)  
  
-   En un sistema de 64 bits:  
  
     C:\Archivos de programa[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
     \- O BIEN -  
  
     \<Directorio de características compartidas (x86)>\Tools\\(directorio de características compartidas (x86) alternativo proporcionado por el usuario)  
  
### <a name="to-install-distributed-replay-features"></a>Para instalar las características de Distributed Replay  
  
1.  Para iniciar la instalación de cualquiera de las características de Distributed Replay, inicie el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
2.  La página **Reglas auxiliares del programa de instalación** identifica los problemas que pueden producirse en la instalación de los archivos auxiliares del programa de instalación de SQL Server. Debe corregir los errores debidos a esos problemas antes de continuar con la instalación.  
  
3.  En la página **Clave del producto** , seleccione un botón de opción para indicar si está instalando una edición gratuita de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o una versión de producción del producto con una clave de PID. Para obtener más información, vea [ediciones y componentes de SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
4.  En la página **términos de licencia** , lea el contrato de licencia y, a continuación, active la casilla para aceptar los términos y condiciones de la licencia. Para ayudar a mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], también puede habilitar la opción de uso de características y enviar informes a [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
5.  En la página **Archivos auxiliares del programa de instalación** , haga clic en **Instalar** para instalar o actualizar los archivos auxiliares del programa de instalación para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  En la **Página rol de instalación** , seleccione ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalación de características**y, a continuación, haga clic en **siguiente** para continuar en la página selección de **características** .  
  
7.  En la página **Selección de características** , configure las características que desea instalar.  
  
    -   Para instalar la herramienta de administración, seleccione **Herramientas de administración - Básica**.  
  
    -   Para instalar el servicio de controlador, seleccione **Controlador de Distributed Replay**.  
  
    -   Para instalar el servicio de cliente, seleccione **Distributed Replay Client**.  
  
     **Importante**: al configurar Distributed Replay Controller, puede especificar una o más cuentas de usuario que se usarán para ejecutar los servicios Distributed Replay Client. La lista siguiente es una relación de las cuentas admitidas:  
  
    -   Cuenta de usuario de dominio  
  
    -   Cuenta de usuario local creada por el usuario  
  
    -   Administrador  
  
    -   Cuenta virtual y MSA (cuenta de servicio administrada)  
  
    -   Network Services, servicios locales y sistema  
  
     No se aceptan cuentas de grupo (locales o de dominio) y otras cuentas integradas (como Todos).  
  
8.  Opcionalmente, haga clic en el botón de puntos suspensivos (…) para cambiar la ruta de acceso al directorio de características compartidas.  
  
    1.  En equipos de 32 bits, la ruta de instalación predeterminada es **c:\Archivos\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** de programa  
  
    2.  En equipos de 64 bits, la ruta de instalación predeterminada es C:\Archivos de programa **(\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] x86)** .  
  
9. Cuando haya terminado, haga clic en **Siguiente**.  
  
10. En la página **Reglas de instalación** , el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida la configuración del equipo. Una vez completado el proceso de validación, haga clic en **Siguiente**.  
  
11. La página **requisitos de espacio en disco** calcula el espacio en disco necesario para las características que especifique. A continuación, compara el espacio necesario con el espacio en disco disponible.  
  
12. En la página **Informes de errores** , especifique la información que desee enviar a [!INCLUDE[msCoName](../../includes/msconame-md.md)] para ayudar a mejorar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, se habilita la opción de informe de errores.  
  
13. En la página **Reglas de configuración de instalación** , el Comprobador de configuración del sistema ejecutará uno o varios conjuntos de reglas para validar la configuración del equipo con las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que haya especificado.  
  
14. En la página **Preparado para instalar el programa**, haga clic en **Instalar**.  
  
    > [!IMPORTANT]  
    >  Después de instalar Distributed Replay, debe crear las reglas de firewall en los equipos cliente y de controlador, y conceder a cada equipo cliente permisos en el servidor de destino. Para obtener más información, vea [Completar los pasos posteriores a la instalación](../../tools/distributed-replay/complete-the-post-installation-steps.md).  
  
 En estos temas adicionales se documentan otras maneras de instalar Distributed Replay:  
  
-   [Instalación de Distributed Replay desde el símbolo del sistema](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [Instalación de Distributed Replay mediante un archivo de configuración](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
 Debe disponer de permisos administrativos para instalar cualquiera de las características de Distributed Replay. Solo un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con permisos sysadmin puede agregar las cuentas del servicio de cliente al rol de servidor sysadmin del servidor de prueba. Para obtener más información sobre las consideraciones de seguridad de Distributed Replay, vea [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte también  
 [Características admitidas por las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Requisitos de Distributed Replay](../../tools/sql-server-profiler/replay-requirements.md)   
 [Opciones de la línea de comandos de la herramienta de administración &#40;Distributed Replay utilidad&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurar Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
