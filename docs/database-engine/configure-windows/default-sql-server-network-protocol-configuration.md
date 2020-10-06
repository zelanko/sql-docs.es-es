---
title: Configuración predeterminada del protocolo de red de SQL Server | Microsoft Docs
description: Vea los factores que afectan a la activación o desactivación de los protocolos de red durante la instalación de SQL Server. Vea cómo configurar protocolos después de la instalación.
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], default settings
- default protocols, after install
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d5463ac163271cf14f5b52167559bc8f3f53d805
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671118"
---
# <a name="default-sql-server-network-protocol-configuration"></a>Configuración predeterminada de protocolo de red de SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Para mejorar la seguridad, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deshabilita la conectividad de red de algunas instalaciones nuevas. La conectividad de red a través de TCP/IP no se deshabilitará si se usa la edición Enterprise, Standard, Evaluation o Workgroup, o si hay una instalación anterior de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. El protocolo de memoria compartida se habilita para todas las instalaciones con el fin de permitir las conexiones locales con el servidor. Puede que el servicio Explorador de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se detenga, según las condiciones y opciones de instalación.

Use el nodo Configuración de red de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] del Administrador de configuración de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para configurar los protocolos de red tras la instalación. Use el nodo Servicios de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] del Administrador de configuración de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para configurar el servicio Explorador de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de modo que se inicie automáticamente. Para más información, consulte [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


## <a name="default-configuration"></a>Configuración predeterminada

En la tabla siguiente se describe la configuración tras la instalación.

|Edición | Nueva instalación e instalación anterior presente | Memoria compartida | TCP/IP | Canalizaciones con nombre|
| -------- | -- | -- | -- | --  |  
|Enterprise | Nueva instalación | habilitado | habilitado | Deshabilitadas para las conexiones de red.|
|Estándar | Nueva instalación | habilitado | habilitado | Deshabilitadas para las conexiones de red.|
|Web | Nueva instalación | habilitado | habilitado | Deshabilitadas para las conexiones de red.|
|Desarrollador | Nueva instalación | habilitado | Disabled | Deshabilitadas para las conexiones de red.|
|Evaluación | Nueva instalación | habilitado | habilitado | Deshabilitadas para las conexiones de red.|
|SQL Server Express | Nueva instalación | habilitado | Disabled | Deshabilitadas para las conexiones de red.|
|Todas las ediciones | Hay una instalación anterior presente, pero no se actualiza. | Igual que en una instalación nueva | Igual que en una instalación nueva | Igual que en una instalación nueva|
|Todas las ediciones | Actualizar | habilitado | Se conserva la configuración de la instalación anterior. | Se conserva la configuración de la instalación anterior.|


>[!NOTE]
> Si la instancia se ejecuta en un clúster de conmutación por error de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], escucha en los puertos de cada dirección IP seleccionada para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] durante la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
>[!NOTE]
> Si está instalando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] con argumentos del símbolo del sistema, puede especificar los protocolos que se habilitarán mediante el uso de los parámetros `TCPENABLED` y `NPENABLED` . Para más información, consulte [Instalar SQL Server 2016 desde el símbolo del sistema](../install-windows/install-sql-server-from-the-command-prompt.md).

## <a name="creating-a-connection-string"></a>Creación de una cadena de conexión

Consulte los temas siguientes para ver ejemplos de cadenas de conexión:
* [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [Crear una cadena de conexión válida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)



## <a name="ssnoversion_md-browser-settings"></a>[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Configuración del explorador

El servicio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser se puede configurar para que se inicie automáticamente durante la instalación. El inicio automático es la opción predeterminada en las siguientes condiciones:

* Cuando se actualiza una instalación.
* Cuando se instala en paralelo con otra instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
* Cuando se instala en un clúster.
* Cuando se instala una instancia con nombre del motor de base de datos que incluye todas las instancias de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express.
* Cuando se instala una instancia con nombre de Analysis Services.

## <a name="see-also"></a>Consulte también

[Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)

[Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)