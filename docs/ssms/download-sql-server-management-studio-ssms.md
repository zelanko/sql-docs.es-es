---
title: Descargar SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "instalar ssms, descargar ssms, versiones de ssms más recientes"
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- "instalación de sql management studio"
- descargar sql management studio
- ms sql management studio
- instalar sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 8c43f57c6d40d3f2c29f220581dddcf74bf96287
ms.contentlocale: es-es
ms.lasthandoff: 07/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Descarga de SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a SQL Database. SSMS proporciona herramientas para configurar, supervisar y administrar instancias de SQL Server desde cualquier lugar que las implemente. Con SSMS puede implementar, supervisar y actualizar los componentes de capa de datos usados por las aplicaciones, además de compilar consultas y scripts. 

Esta versión presenta una compatibilidad mejorada con las versiones anteriores de SQL Server, un instalador web independiente y notificaciones del sistema dentro de SSMS a medida que nuevas versiones estén disponibles.  
  
![descarga](../ssdt/media/download.png) SSMS es gratuito. **[Descargar SQL Server Management Studio 17.1](https://go.microsoft.com/fwlink/?linkid=849819)** SSMS 17.X es la generación más reciente de SQL Server Management Studio y proporciona compatibilidad con SQL Server 2017. 

![descarga](../ssdt/media/download.png) **[Descargar el paquete de actualización de SQL Server Management Studio 17.1 (actualización de la versión 17.0 a la 17.1)](https://go.microsoft.com/fwlink/?linkid=849821)**

> [!NOTE]
> El módulo SQL Server PowerShell se instala ahora de forma independiente a través de la Galería de PowerShell.  Para más información, vea las [instrucciones de descarga](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**Información de versión**  
  
Número de versión: 17.1  
Número de compilación para esta versión: 14.0.17119.0

## <a name="new-in-this-release"></a>Nuevo en esta versión  

SSMS 17.1 es la primera actualización de la generación 17.X de SQL Server Management Studio.  La generación 17.X proporciona compatibilidad con casi todas las áreas de características de SQL Server 2008 a SQL Server 2017.  La versión 17.X es también la generación de SSMS que admite PaaS de SQL Analysis Service.

La versión 17.1 incluye:

* Correcciones de varios problemas notificados por los usuarios 
* Una nueva herramienta de administración de escalado horizontal de Integration Services

Para obtener una lista completa de los cambios, vea   
                [SQL Server Management Studio - Changelog (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
   
Para más información sobre la colección de datos de usuario, consulte   
                [Declaración de privacidad de SQL Server](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx) 
  
## <a name="supported-sql-offerings"></a>Ofertas de SQL admitidas
  
* Esta versión de SSMS funciona con todas las [versiones compatibles de SQL Server 2008 - SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044) y proporciona el mayor nivel de compatibilidad para trabajar con las últimas características de nube en Azure SQL Database y en Azure SQL Data Warehouse.  
* No hay ningún bloqueo explícito para SQL Server 2000 o SQL Server 2005, pero es posible que algunas características no funcionen correctamente.  
* Además, SSMS 17.X puede instalarse en paralelo con SSMS 16.X o SQL Server 2014 SSMS y versiones anteriores. 
  
## <a name="supported-operating-systems"></a>Sistemas operativos admitidos
  
Esta versión de SSMS admite las siguientes plataformas cuando se usa con el Service Pack más reciente disponible:   
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 (SP1)
- Windows Server 2016
- Windows Server 2012 (64 bits) 
- Windows Server 2012 R2 (64 bits) 
- Windows Server 2008 R2 (64 bits)  

>[!NOTE]
>SSMS 17.X se basa en el shell aislado de Visual Studio 2015, que se lanzó antes que Windows Server 2016. Microsoft se toma en serio la compatibilidad entre aplicaciones y garantiza que las aplicaciones ya publicadas sigan funcionando en las últimas versiones de Windows. Para minimizar los problemas de ejecución de SSMS en Windows Server 2016, asegúrese de que SSMS tiene aplicadas todas las actualizaciones más recientes. Si experimenta problemas con SSMS en Windows Server 2016, póngase en contacto con soporte técnico. El equipo de soporte técnico determina si el problema es con SSMS, Visual Studio o con la compatibilidad de Windows. A continuación, dirige el problema al equipo adecuado para una investigación más exhaustiva.

## <a name="ssms-installation-tips-and-issues"></a>Problemas y sugerencias de instalación de SSMS

>[!NOTE]
> La instalación de SSMS 17.x no actualiza ni reemplaza versiones anteriores de SSMS.  SSMS 17.x se instala en paralelo con versiones anteriores de modo que ambas versiones estén disponibles para su uso.
> Si un equipo contiene instalaciones en paralelo de SSMS, compruebe si inicia la versión correcta para sus necesidades específicas.
>  ![SSMS 17.x](media/ssms-start-menu.png)

**Minimizar los reinicios de instalación**
- Realice las acciones siguientes para reducir las posibilidades de que el programa de instalación de SSMS necesite un reinicio al final de la instalación:
  - Asegúrese de que está ejecutando una versión actualizada de Visual C++ 2013 Redistributable Package. Se necesita la versión 12.00.40649.5 (o superior). Solo se necesita la versión x64.
  - Compruebe que la versión de .NET Framework en el equipo es 4.6.1 (o superior).
  - Cierre otras instancias de Visual Studio que estén abiertas en el equipo.
  - Asegúrese de que todas las actualizaciones más recientes del sistema operativo estén instaladas en el equipo.
  - Las acciones indicadas suelen ser necesarias solo una vez. Hay algunos casos en los que se necesita reiniciar durante las actualizaciones adicionales a la misma versión principal de SSMS. En el caso de las actualizaciones menores, todos los requisitos previos de SSMS ya están instalados en el equipo.

- Para ver la lista de problemas conocidos y soluciones, vea [SQL Server Management Studio: notas de la versión](../ssms/sql-server-management-studio-release-notes.md)

## <a name="available-languages"></a>Idiomas disponibles  
> Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2. 
  
Esta versión de SSMS puede instalarse en los idiomas siguientes:

SQL Server Management Studio 17.1:<br>
[Alemán](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [Chino (China)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [Coreano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [Español](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [Francés](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [Italiano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [Japonés](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [Ruso](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

Paquete de actualización de SQL Server Management Studio 17.1 (actualización de la versión 17.0 a la 17.1):<br>
[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40a)

## <a name="previous-releases"></a>Versiones anteriores  
[Versiones anteriores de SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>Comentarios  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)  
  
## <a name="see-also"></a>Vea también  
[Tutorial: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Documentación de SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[Service Pack y actualizaciones adicionales](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



