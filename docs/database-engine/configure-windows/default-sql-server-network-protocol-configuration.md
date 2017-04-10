---
title: "Configuraci&#243;n predeterminada de protocolo de red de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "07/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "protocolos [SQL Server], configuración predeterminada"
  - "protocolos predeterminados, después de la instalación"
ms.assetid: 635ea361-a797-4971-bd05-e3415862bc5c
caps.latest.revision: 4
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 4
---
# Configuraci&#243;n predeterminada de protocolo de red de SQL Server
Para mejorar la seguridad, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deshabilita la conectividad de red de algunas instalaciones nuevas. La conectividad de red mediante TCP/IP no se deshabilitará si se usa la edición Enterprise, Standard o Workgroup, o si hay una instalación anterior de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. El protocolo de memoria compartida se habilita para todas las instalaciones con el fin de permitir las conexiones locales con el servidor. Puede que el servicio Explorador de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se detenga, según las condiciones y opciones de instalación.

Use el nodo Configuración de red de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] del Administrador de configuración de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para configurar los protocolos de red tras la instalación. Use el nodo Servicios de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] del Administrador de configuración de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para configurar el servicio Explorador de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de modo que se inicie automáticamente. Para más información, consulte [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).


## Configuración predeterminada

En la tabla siguiente se describe la configuración tras la instalación.

Edición | Nueva instalación e instalación anterior presente | Memoria compartida | TCP/IP    | Canalizaciones con nombre
| -------- | -- | -- | -- | --  |  
Enterprise  | Nueva instalación  | Habilitado   | Habilitado   | Deshabilitadas para las conexiones de red.
Standard    | Nueva instalación  | Habilitado   | Habilitado   | Deshabilitadas para las conexiones de red.
Web | Nueva instalación  | Habilitado   | Habilitado   | Deshabilitadas para las conexiones de red.
Desarrollador   | Nueva instalación  | Habilitado   | Deshabilitado  | Deshabilitadas para las conexiones de red.
Evaluation  | Nueva instalación  | Habilitado   | Deshabilitado  | Deshabilitadas para las conexiones de red.
SQL Server Express  | Nueva instalación  | Habilitado   | Deshabilitado  | Deshabilitadas para las conexiones de red.
Todas las ediciones    | Hay una instalación anterior presente, pero no se actualiza.   | Igual que en una instalación nueva  | Igual que en una instalación nueva  | Igual que en una instalación nueva
Todas las ediciones    | Actualización   | Habilitado   | Se conserva la configuración de la instalación anterior.    | Se conserva la configuración de la instalación anterior.


>[!NOTE]
> Si la instancia se ejecuta en un clúster de conmutación por error de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], escuchará en los puertos de cada dirección IP seleccionada para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] durante la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
>[!NOTE]
> Si está instalando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] con argumentos del símbolo del sistema, puede especificar los protocolos que se habilitarán mediante el uso de los parámetros `TCPENABLED` y `NPENABLED`. Para más información, consulte [Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).

## Creación de una cadena de conexión

Consulte los temas siguientes para ver ejemplos de cadenas de conexión:
* [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
* [Crear una cadena de conexión válida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
* [Crear una cadena de conexión válida con canalizaciones con nombre](Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.xml)


## [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Configuración del explorador

El servicio [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Browser se puede configurar para que se inicie automáticamente durante la instalación. El inicio automático es la opción predeterminada en las siguientes condiciones:

* Cuando se actualiza una instalación.
* Cuando se instala en paralelo con otra instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
* Cuando se instala en un clúster.
* Cuando se instala una instancia con nombre del motor de base de datos que incluye todas las instancias de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Express.
* Cuando se instala una instancia con nombre de Analysis Services.

## Vea también

[Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)

[Configuración de Área expuesta](../../relational-databases/security/surface-area-configuration.md)  

