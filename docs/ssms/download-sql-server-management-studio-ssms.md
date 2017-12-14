---
title: Descargar SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
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
caps.latest.revision: "145"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 550f91939f2ab6b8e16455a6a5dea2a4ac519c5d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="download-sql-server-management-studio-ssms"></a>Descarga de SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] SSMS es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a SQL Database. SSMS proporciona herramientas para configurar, supervisar y administrar instancias de SQL. Use SSMS para implementar, supervisar y actualizar los componentes de capa de datos usados por las aplicaciones, además de compilar consultas y scripts.

Use SQL Server Management Studio (SSMS) para consultar, diseñar y administrar bases de datos y almacenes de datos, estén donde estén, en el equipo local o en la nube.

**SSMS es gratuito.**

SSMS 17.x es la generación más reciente de *SQL Server Management Studio* y proporciona compatibilidad con SQL Server 2017.

**[![descargar](../ssdt/media/download.png) Descargar SQL Server Management Studio 17.3](https://go.microsoft.com/fwlink/?linkid=858904)**

**[![descargar](../ssdt/media/download.png) Descargar el paquete de actualización de SQL Server Management Studio 17.3 (actualización de la versión 17.x a la 17.3)](https://go.microsoft.com/fwlink/?linkid=858906)**

La instalación de SSMS 17.x no actualiza ni reemplaza las versiones 16.x de SSMS ni las anteriores. SSMS 17.x se instala en paralelo con versiones anteriores de modo que ambas versiones estén disponibles para su uso.
Si un equipo contiene instalaciones en paralelo de SSMS, compruebe que inicia la versión correcta para sus necesidades específicas. La versión más reciente tiene la etiqueta *Microsoft SQL Server Management Studio 17* y tiene un nuevo icono: 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> El módulo SQL Server PowerShell se instala ahora de forma independiente a través de la Galería de PowerShell.  Para más información, vea las [instrucciones de descarga](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**Información de versión**

Número de versión: 17.3

Número de compilación de esta versión: 14.0.17199.0

## <a name="new-in-this-release"></a>Nuevo en esta versión

SSMS 17.3 es la versión más reciente de SQL Server Management Studio. La generación 17.x de SSMS proporciona compatibilidad con casi todas las áreas de características de SQL Server 2008 a SQL Server 2017. La versión 17.x también es compatible con PaaS de SQL Analysis Services.

La versión 17.3 incluye:

- Se ha agregado el nuevo asistente "Importar archivo plano" para simplificar la experiencia de importación de archivos CSV con un marco de trabajo inteligente, que ahora no exige prácticamente intervención por parte del usuario ni poseer conocimientos especializados sobre dominios. Para obtener detalles, vea [Importación de archivos planos mediante el asistente de SQL](../relational-databases/import-export/import-flat-file-wizard.md).
- Se ha agregado el nodo "XEvent Profiler" al Explorador de objetos. Para obtener detalles, vea [Uso de XEvent Profiler de SSMS](../relational-databases/extended-events/use-the-ssms-xe-profiler.md).
- Se han actualizado el filtrado y la categorización de esperas en el informe histórico de esperas del panel de rendimiento.
- Se ha agregado la comprobación de sintaxis de la función "Predict".
- Se ha agregado la comprobación de sintaxis de las consultas de administración de biblioteca externa.
- Se ha agregado compatibilidad con SMO a la administración de biblioteca externa.
- Se ha agregado compatibilidad con "Iniciar PowerShell" a la ventana "Servidores registrados" (se requiere un nuevo módulo de SQL PowerShell).
- Always On: se ha agregado [compatibilidad de enrutamiento de solo lectura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md) a los grupos de disponibilidad.
- Se ha agregado una opción para enviar detalles de seguimiento a la ventana de salida de los inicios de sesión "Active Directory - Universal compatible con MFA" (desactivados de forma predeterminada; deben activarse en la configuración de usuario, en "Herramientas > Opciones > Servicios de Azure > Nube de Azure > Nivel de seguimiento de la ventana de salida de ADAL"). 
- Almacén de consultas: 
  - La interfaz de usuario del almacén de consultas será accesible aunque QDS esté desactivado, siempre que haya registrado datos.
  - La interfaz de usuario del almacén de consultas ahora expone la categorización de esperas en todos los informes existentes. Esto permite que los clientes desbloqueen los escenarios de consultas que más esperan y muchos otros.
- Se ha convertido en opcional la inclusión de los encabezados de parámetros de scripting (desactivada de forma predeterminada; se puede habilitar en la configuración de usuario, en "Herramientas > Opciones > Explorador de objetos de SQL Server > Scripting > Incluir encabezado de parámetros de scripting"). [Artículo de Connect 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).
- Se ha quitado la personalización de marca "RC".

Para ver la lista completa de cambios, consulte [SQL Server Management Studio: Registro de cambios (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md).

Para obtener información sobre la recopilación de datos de usuario, consulte [Declaración de privacidad de SQL Server](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).

## <a name="supported-sql-offerings"></a>Ofertas de SQL admitidas

* Esta versión de SSMS funciona con todas las [versiones compatibles de SQL Server 2008 - SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044) y proporciona el mayor nivel de compatibilidad para trabajar con las últimas características de nube en Azure SQL Database y en Azure SQL Data Warehouse.
* No hay ningún bloqueo explícito para SQL Server 2000 o SQL Server 2005, pero es posible que algunas características no funcionen correctamente.
* Además, SSMS 17.x puede instalarse en paralelo con SSMS 16.x o SQL Server 2014 SSMS y versiones anteriores.

## <a name="supported-operating-systems"></a>Sistemas operativos admitidos
  
Esta versión de SSMS admite las siguientes plataformas de 64 bits cuando se usa con el Service Pack más reciente disponible:
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1) (64 bits)
- Windows Server 2016 *
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

\* SSMS 17.x se basa en el shell aislado de Visual Studio 2015, que se lanzó antes que Windows Server 2016. Microsoft se toma en serio la compatibilidad entre aplicaciones y garantiza que las aplicaciones ya publicadas sigan funcionando en las últimas versiones de Windows. Para minimizar los problemas de ejecución de SSMS en Windows Server 2016, asegúrese de que SSMS tiene aplicadas todas las actualizaciones más recientes. Si experimenta problemas con SSMS en Windows Server 2016, póngase en contacto con soporte técnico. El equipo de soporte técnico determina si el problema es con SSMS, Visual Studio o con la compatibilidad de Windows. A continuación, dirige el problema al equipo adecuado para una investigación más exhaustiva.

## <a name="ssms-installation-tips-and-issues"></a>Problemas y sugerencias de instalación de SSMS

### <a name="minimize-installation-reboots"></a>Minimizar los reinicios de instalación

* Realice las acciones siguientes para reducir las posibilidades de que el programa de instalación de SSMS necesite un reinicio al final de la instalación:
  * Asegúrese de que está ejecutando una versión actualizada de Visual C++ 2013 Redistributable Package. Se necesita la versión 12.00.40649.5 (o superior). Solo se necesita la versión x64.
  * Compruebe que la versión de .NET Framework en el equipo es 4.6.1 (o superior).
  * Cierre otras instancias de Visual Studio que estén abiertas en el equipo.
  * Asegúrese de que todas las actualizaciones más recientes del sistema operativo estén instaladas en el equipo.
  * Las acciones indicadas suelen ser necesarias solo una vez. Hay algunos casos en los que se necesita reiniciar durante las actualizaciones adicionales a la misma versión principal de SSMS. En el caso de las actualizaciones menores, todos los requisitos previos de SSMS ya están instalados en el equipo.

* Para ver la lista de problemas conocidos y soluciones, vea [SQL Server Management Studio: notas de la versión](../ssms/sql-server-management-studio-release-notes.md)

## <a name="available-languages"></a>Idiomas disponibles

> [!NOTE]
> Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.

Esta versión de SSMS puede instalarse en los idiomas siguientes:

SQL Server Management Studio 17.3:<br>
[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)

Paquete de actualización de SQL Server Management Studio 17.3 (actualización de la versión 17.x a la 17.3):<br>
[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40a)

## <a name="release-notes"></a>Notas de la versión

A continuación, se muestran problemas y limitaciones con esta versión 17.3:

**SSMS general**

- La siguiente funcionalidad de SSMS no es compatible con la autenticación de Azure AD mediante UA con MFA:
   - El Asistente para la optimización de motor de base de datos no es compatible con la autenticación de Azure AD; hay un problema conocido que consiste en que el mensaje de error que se presenta al usuario es un poco críptico: "No se puede cargar el archivo o ensamblado 'Microsoft.IdentityModel.Clients.ActiveDirectory,..." en lugar del esperado: "El Asistente para la optimización de motor de base de datos no admite Microsoft Azure SQL Database. (DTAClient)".
- Al intentar analizar una consulta en DTA se produce un error: "El objeto debe implementar IConvertible. (mscorlib)".
- *Consultas con regresión* no aparece en la lista Almacén de consultas de informes del Explorador de objetos.
   - Solución: haga clic con el botón derecho en el nodo **Almacén de consultas** y seleccione **Ver consultas con regresión**.

**Integration Services (IS)**

- La [execution_path] de [catalog].[event_messagea] no es correcta para ejecuciones de paquetes en Escalabilidad horizontal. [execution_path] comienza con "\Package" en lugar del nombre de objeto del ejecutable del paquete. Al ver el informe general sobre ejecuciones de paquetes en SSMS, el vínculo de "Ruta de acceso de ejecución" de Información general de ejecución no puede funcionar. La solución es hacer clic en "Ver mensajes" en el informe general para comprobar todos los mensajes de eventos.



## <a name="previous-releases"></a>Versiones anteriores

[Versiones anteriores de SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Comentarios

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>Vea también

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentación de SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Service Pack y actualizaciones adicionales](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
