---
title: Configuración de red de cliente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: bd28758b2f5cb0c5e98ea8b24784369386e7bdce
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799535"
---
# <a name="client-network-configuration"></a>Configuración de red de cliente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El software de cliente permite que los equipos cliente se conecten a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de una red. Un "cliente" es una aplicación front-end que utiliza los servicios que proporciona un servidor, por ejemplo, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. El equipo que hospeda esta aplicación recibe el nombre de *equipo cliente*.  
  
 En su nivel más sencillo, un cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede residir en el mismo equipo que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, normalmente un cliente se conecta a uno o más servidores remotos mediante una red. La arquitectura cliente/servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite administrar sin ningún problema varios clientes y servidores de una red. Las configuraciones cliente predeterminadas son suficientes en la mayoría de los casos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden incluir aplicaciones de diversos tipos, por ejemplo:  
  
-   Consumidores OLE DB  
  
     Estas aplicaciones utilizan el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proveedor OLE DB media entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones cliente que consumen datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como conjuntos de filas OLE DB. La utilidad de símbolo del sistema **sqlcmd** y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]son ejemplos de aplicaciones OLE DB.  
  
-   aplicaciones ODBC  
  
     Estas aplicaciones incluyen utilidades de cliente instaladas con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como por ejemplo la utilidad del símbolo del sistema **osql** , así como otras aplicaciones que usan el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Clientes de DB-Library  
  
     Estas aplicaciones incluyen la utilidad de símbolo del sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** y clientes escritos en DB-Library. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La compatibilidad de las aplicaciones cliente que usan DB-Library se limita a las características de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.  
  
> [!NOTE]  
>  Aunque [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] sigue admitiendo conexiones de las aplicaciones existentes mediante las API DB-Library y SQL incrustado, no incluye los archivos ni la documentación necesarios para realizar los trabajos de programación en aplicaciones que utilizan estas API. Una versión futura del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eliminará la compatibilidad para las conexiones desde aplicaciones de DB-Library o Embedded SQL. No utilice DB-Library ni Embedded SQL para desarrollar nuevas aplicaciones. Quite las dependencias de DB-Library o SQL incrustado para modificar las aplicaciones existentes. En lugar de estas API, use el espacio de nombres SQLClient o una API como OLE DB u ODBC. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no incluye la DLL DB-Library necesaria para ejecutar estas aplicaciones. Para ejecutar aplicaciones de DB-Library o SQL incrustado, debe estar disponible la DLL de DB-Library de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 6.5, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 Independientemente del tipo de aplicación, la administración de clientes consiste principalmente en configurar su conexión con los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Según los requisitos del sitio, la administración de los clientes puede variar desde poco más que especificar el nombre del equipo servidor hasta generar una biblioteca de entradas de configuración personalizadas para ajustarse a un entorno multiservidor variado.  
  
 La DLL de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client contiene las bibliotecas de red y es instalada por el programa de instalación. Los protocolos de red no se habilitan durante la configuración de las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las instalaciones actualizadas habilitan los protocolos habilitados anteriormente. Los protocolos de red subyacentes se instalan como parte de la instalación de Windows (también puede instalarlos mediante el subprograma Red del Panel de control). Para administrar los clientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilizan las siguientes herramientas:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Administrador de configuración  
  
     Los componentes de red tanto del cliente como del servidor se administran mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que combina la Herramienta de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la Herramienta de red de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el Administrador de servicios de versiones anteriores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Administrador de configuración es un complemento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC). También aparece como un nodo en el complemento de Administración de equipos de Windows. El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sirve para habilitar, deshabilitar, configurar y otorgar el grado de prioridad a bibliotecas de red individuales.  
  
-   ssNoVersion  
  
     Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar los componentes de red en un equipo cliente. Es posible habilitar o deshabilitar las bibliotecas de red individuales durante la instalación cuando ésta se inicia desde el símbolo del sistema.  
  
-   Administrador de orígenes de datos ODBC  
  
     El Administrador de orígenes de datos ODBC le permite crear y modificar orígenes de datos ODBC en equipos que ejecutan el sistema operativo Microsoft Windows.  
  
## <a name="in-this-section"></a>En esta sección  
 [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md)  
  
 [Crear o eliminar un alias de servidor para que lo utilice un cliente &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [Iniciar una sesión en SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
 [Abrir el Administrador de orígenes de datos ODBC](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
 [Comprobar la versión del controlador ODBC de SQL Server &#40;Windows&#41;](../../database-engine/configure-windows/check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Configuración de red del servidor](../../database-engine/configure-windows/server-network-configuration.md)  
  
 [Administrar el servicio del motor de base de datos](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
