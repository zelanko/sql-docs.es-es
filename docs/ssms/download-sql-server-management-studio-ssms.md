---
title: Descargar SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
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
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: a689293fadb1a442f94d88cc06a9e7a4ef06650f
ms.contentlocale: es-es
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Descarga de SQL Server Management Studio (SSMS)

SSMS es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a SQL Database. SSMS proporciona herramientas para configurar, supervisar y administrar instancias de SQL. Use SSMS para implementar, supervisar y actualizar los componentes de capa de datos usados por las aplicaciones, además de compilar consultas y scripts.

Use SQL Server Management Studio (SSMS) para consultar, diseñar y administrar bases de datos y almacenes de datos, estén donde estén, en el equipo local o en la nube.

**SSMS es gratuito.**

SSMS 17.x es la generación más reciente de *SQL Server Management Studio* y proporciona compatibilidad con SQL Server 2017.

**[![descarga](../ssdt/media/download.png) Descargar SQL Server Management Studio 17.2](https://go.microsoft.com/fwlink/?linkid=854085)**

**[![descarga](../ssdt/media/download.png) Descargar el paquete de actualización de SQL Server Management Studio 17.2 (actualización de la versión 17.x a la 17.2)](https://go.microsoft.com/fwlink/?linkid=854087)**

La instalación de SSMS 17.x no actualiza ni reemplaza las versiones 16.x de SSMS ni las anteriores. SSMS 17.x se instala en paralelo con versiones anteriores de modo que ambas versiones estén disponibles para su uso.
Si un equipo contiene instalaciones en paralelo de SSMS, compruebe que inicia la versión correcta para sus necesidades específicas. La versión más reciente tiene la etiqueta *Microsoft SQL Server Management Studio 17* y tiene un nuevo icono: 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> El módulo SQL Server PowerShell se instala ahora de forma independiente a través de la Galería de PowerShell.  Para más información, vea las [instrucciones de descarga](download-sql-server-ps-module.md).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**Información de versión**

Número de versión: 17.2 Número de compilación para esta versión: 14.0.17177.0

## <a name="new-in-this-release"></a>Nuevo en esta versión

SSMS 17.2 es la versión más reciente de SQL Server Management Studio. La generación 17.x de SSMS proporciona compatibilidad con casi todas las áreas de características de SQL Server 2008 a SQL Server 2017. La versión 17.x también es compatible con PaaS de SQL Analysis Services.

La versión 17.2 incluye:

- Multi-Factor Authentication (MFA)
  - Autenticación de Azure AD de varios usuarios para la autenticación universal con Multi-Factor Authentication (UA con MFA)
  - Se ha agregado un nuevo campo de entrada de credenciales de usuario para la autenticación universal con MFA a fin de permitir la autenticación de varios usuarios.
- El cuadro de diálogo de conexión ahora admite los siguientes cinco métodos de autenticación:
  - Autenticación de Windows
  - Autenticación de SQL Server
  - Active Directory: Universal compatible con MFA
  - Active Directory: Contraseña
  - Active Directory: Integrado

- El asistente para importación y exportación de bases de datos para DacFx ahora puede usar la autenticación universal con MFA.
- Para obtener información sobre la compatibilidad de API, consulte [IUniversalAuthProvider Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx) (Interfaz IUniversalAuthProvider).
- La biblioteca administrada de ADAL que usa la autenticación universal de Azure AD con MFA se ha actualizado a la versión 3.13.9.
- Una nueva interfaz de CLI compatible con la configuración de administración de Azure AD para SQL Database y SQL Data Warehouse.

 Para obtener más información sobre los métodos de autenticación de Active Directory, vea [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) y [Configurar Multi-Factor Authentication de Azure SQL Database para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- La ventana de salida tiene entradas para las consultas que se ejecutan durante la expansión de los nodos del Explorador de objetos.
- Diseñador de vistas habilitado para instancias de Azure SQL Database
- Han cambiado las opciones de scripting predeterminadas para incluir en script objetos desde el Explorador de objetos en SSMS:
  - Anteriormente, el valor predeterminado en una instalación nueva era que el destino de script generado tuviera la versión más reciente de SQL Server (actualmente, SQL Server 2017).
  - En SSMS 17.2 se ha agregado una nueva opción: *Coincidir configuración del script con origen*. Cuando se establece en *True*, el script generado tiene como destino la misma versión, tipo de motor y edición del motor que el servidor al que pertenece el objeto del que se crea el script.
  - El valor *Coincidir configuración del script con origen* se establece en *True* de forma predeterminada, por lo que las nuevas instalaciones de SSMS tendrán automáticamente la opción predeterminada de crear siempre el script de los objetos en el mismo destino que el servidor original.
  - Cuando el valor *Coincidir configuración del script con origen* se establece en *False*, se habilitarán las opciones de destino de scripting normales y funcionarán como lo hacían anteriormente.
  - Además, todas las opciones de scripting se han movido a su propia sección: *Opciones de versión*. Ya no están en *Opciones generales de scripting*.

- Se ha agregado compatibilidad con nubes nacionales en "Restore from URL".
- Los informes de QueryStoreUI ahora son compatibles con otras métricas (RowCount, DOP, tiempo de CLR, etc.) de sys.query_store_runtime_stats.
- IntelliSense ahora es compatible con Azure SQL Database.
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- El cuadro de diálogo Seguridad: conexión tendrá como valor predeterminado no confiar en certificados de servidor y solicitará cifrado para las conexiones de Azure SQL Database.
- Mejoras generales sobre la compatibilidad de SQL Server con Linux:
 - Se recupera el nodo Correo electrónico de base de datos.
 - Se han solucionado algunos problemas relacionados con las rutas de acceso
 - Mejoras de estabilidad del Monitor de actividad
 - El cuadro de diálogo Propiedades de conexión muestra la plataforma correcta
- El informe del servidor del panel de rendimiento ahora está disponible como informe predeterminado:
  - Puede conectarse a SQL Server 2008 y versiones más recientes.
  - El subinforme Índices que faltan usa la puntuación para ayudar a identificar los índices más útiles.
  - El subinforme de estadísticas de esperas históricas ahora agrega esperas por categoría. Las esperas Inactivo y En suspensión se filtran de forma predeterminada.
  - Nuevo subinforme Bloqueos temporales del historial.
- La búsqueda del nodo Plan de presentación permite buscar en las propiedades del plan. Busque fácilmente cualquier propiedad de operador como el nombre de la tabla. Para usar esta opción al ver un plan:
  - Haga clic con el botón derecho en el plan y, en el menú contextual, haga clic en la opción Buscar nodo.
  - Use CTRL+F.

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

SQL Server Management Studio 17.2:<br>
[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

Paquete de actualización de SQL Server Management Studio 17.2 (actualización de la versión 17.x a la 17.2):<br>
[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40a)

## <a name="release-notes"></a>Notas de la versión

A continuación, se muestran problemas y limitaciones con esta versión 17.2:

- Las ventanas de consulta que usan la autenticación "Active Directory - Universal compatible con MFA" pueden experimentar un error similar al siguiente, al intentar ejecutar una consulta después de que esté abierta durante una hora o más:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of *ConnectRetryCount* to increase the number of recovery attempts.`

   Si se vuelve a ejecutar la consulta, se debería solucionar el error y realizar correctamente.

- No se admite la siguiente funcionalidad de SSMS para Azure AD mediante la autenticación universal con MFA:
  - El diseñador **Nueva tabla o vista** muestra el aviso de inicio de sesión antiguo y no funciona para la autenticación de Azure AD.
  - La característica **Editar las primeras 200 filas** no es compatible con la autenticación de Azure AD.
  - El componente **Servidor registrado** no es compatible con la autenticación de Azure AD.
  - El **Asistente para la optimización de motor de base de datos** no es compatible con la autenticación de Azure AD. Hay un problema conocido en el que el mensaje de error que se presenta al usuario no es nada útil: *No se puede cargar el archivo o ensamblado 'Microsoft.IdentityModel.Clients.ActiveDirectory,...* en lugar del que se espera *El Asistente para la optimización de motor de base de datos no admite Microsoft Azure SQL Database. (DTAClient)*.

**AS**

- El Explorador de objetos de SSAS no mostrará el nombre de usuario de autenticación de Windows en las propiedades de conexión de Azure AS.
Para obtener más información, vea el [registro de cambios de SSMS](sql-server-management-studio-changelog-ssms.md).

## <a name="previous-releases"></a>Versiones anteriores

[Versiones anteriores de SQL Server Management Studio](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>Comentarios

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>Vea también

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentación de SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Service Pack y actualizaciones adicionales](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

