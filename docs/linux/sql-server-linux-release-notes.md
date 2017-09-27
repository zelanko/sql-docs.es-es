---
title: "Notas de la versión de SQL Server 2017 en Linux | Documentos de Microsoft"
description: "Este tema contiene las notas de la versión y características admitidas en SQL Server 2017 ejecutando en Linux. Notas de la versión se incluyen para RC2 y versiones anteriores."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/07/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 14277304baaaf6aa40fe279af407c7ce915eaa60
ms.contentlocale: es-es
ms.lasthandoff: 09/25/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de la versión de SQL Server 2017 en Linux

Las siguientes notas se aplican a SQL Server 2017 ejecutando en Linux. Esta versión admite muchas de las características del motor de base de datos de SQL Server para Linux. El siguiente tema se divide en secciones para cada versión, desde la versión más reciente, RC2. Ver la información en cada sección completa para las plataformas admitidas, herramientas, características y problemas conocidos.

En la tabla siguiente se enumera las versiones de SQL Server 2017 se tratan en este tema.

| Versión | Versión | Fecha de lanzamiento |
|-----|-----|-----|
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| [CTP 2.1](#ctp21) | 14.0.600.250 | 5-2017 |
| [EN CTP 2.0](#ctp20) | 14.0.500.272 | 4-2017 |
| [CTP 1.4](#ctp14) | 14.0.405.198 | 3-2017 |
| [CTP 1.3](#ctp13) | 14.0.304.138 | 2-2017 |
| [CTP 1.2](#ctp12) | 14.0.200.24 | 1-2017 |
| [CTP 1.1](#ctp11) | 14.0.100.187 | 12-2016 |
| [CTP 1.0](#ctp10) | 14.0.1.246 | 11-2016 |

## <a id="RC2"></a>RC2 (agosto de 2017)

La versión del motor de SQL Server para esta versión es 14.0.900.75.

### <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE]
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1,5 TB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete

En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.900.75-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.900.75-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.900.75-1 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.900.75-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.900.75-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.900.75-1_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.900.75-1_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | más reciente |

### <a name="Unsupported"></a>Servicios y características no admitidas

Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación transaccional |
| &nbsp; | Replicación de mezcla |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida con conexiones 3ª parte |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| &nbsp; | Extensión del grupo de búferes |
| **Agente SQL Server** |  Subsistemas: CmdExec, PowerShell, lector de cola, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de registro del LOG |
| &nbsp; | Captura de datos modificados |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Administración extensible de claves |
| **Servicios de** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos

En las siguientes secciones se describen los problemas conocidos con esta versión de SQL Server de 2017 RC2 en Linux.

#### <a name="general"></a>General

- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- El idioma predeterminado de la **sa** inicio de sesión es el inglés.

    - **Resolución**: cambiar el idioma de la **sa** inicio de sesión con la **ALTER LOGIN** instrucción.

#### <a name="databases"></a>Bases de datos

- No se puede mover la base de datos maestra con la utilidad mssql-conf. Otras bases de datos del sistema pueden aplicarse con mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

- Algunos algoritmos (conjuntos de cifrado) para la seguridad de capa de transporte (TLS) no funcionan correctamente con SQL Server en Linux. Esto da como resultado errores de conexión al intentar conectarse a SQL Server, así como problemas para establecer conexiones entre réplicas en los grupos de alta disponibilidad.

   - **Resolución**: modificar el **mssql.conf** script de configuración de SQL Server en Linux para deshabilitar conjuntos de cifrado problemático, mediante las acciones siguientes:

      1. Agregue lo siguiente al /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers=ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

      1. Reinicie SQL Server con el siguiente comando.
   
      ```
      sudo systemctl restart mssql-server
      ```

- No se puede restaurar las bases de datos de SQL Server 2014 en Windows que use OLTP en memoria en SQL Server 2017 en Linux. Para restaurar una base de datos de SQL Server 2014 que utiliza OLTP en memoria, actualizar las bases de datos a SQL Server 2016 o 2017 de SQL Server en Windows antes de pasar a SQL Server en Linux a través de copia de seguridad/restauración o separar y adjuntar.

#### <a name="remote-database-files"></a>Archivos de base de datos remota

- Hospedar los archivos de base de datos en un servidor NFS no se admite en esta versión. Esto incluye el uso de NFS para agrupación en clústeres, así como las bases de datos en instancias no clúster de conmutación por error de disco compartido. Estamos trabajando en habilitar la compatibilidad de servidor NFS en las próximas versiones.

#### <a name="localization"></a>Localización

- Si no, la configuración regional es inglés (en_us) durante la instalación, debe usar la codificación UTF-8 en su sesión intensiva de errores/terminal. Si utiliza la codificación ASCII, verá un mensaje de error similar al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no puede utilizar la codificación UTF-8, ejecute el programa de instalación mediante la variable de entorno MSSQL_LCID para especificar la opción de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name="full-text-search"></a>Búsqueda de texto completo
- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
Puede ejecutar paquetes SSIS en Linux. Para obtener más información, vea los siguientes artículos:
-   [Anuncio de entrada de blog compatibilidad con SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

Tenga en cuenta los siguientes problemas conocidos con esta versión.

- El **mssql server es** paquete es compatible con Ubuntu y Red Hat Enterprise Linux (RHEL) en esta versión.

- Con SSIS al actualizar los Linux CTP 2.1 y versiones posteriores, paquetes SSIS pueden usar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el servidor SQL Server y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador de ODBC Unicode que se ajusta a la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede utilizar la autenticación de Windows. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Las siguientes características no se admiten en esta versión, al ejecutar paquetes SSIS en Linux:
  - Base de datos de catálogo de SSIS
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - Ampliación SSIS
  - Feature Pack de Azure para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- Almacén de datos de administración (MDW) y el recopilador de datos en SSMS no son compatibles. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- No se puede modificar el número de archivos de registro que se va a conservar.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="RC1"></a>RC1 (julio de 2017)
La versión del motor de SQL Server para esta versión es 14.0.800.90.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE]
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1 TB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.800.90-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.800.90-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.800.90-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.800.90-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.800.90-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.800.90-2_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.800.90-2_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | más reciente |

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación transaccional |
| &nbsp; | Replicación de mezcla |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | Servicios de aprendizaje automático |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Agente SQL Server** |  Subsistemas: CmdExec, PowerShell, lector de cola, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de registro del LOG |
| &nbsp; | Captura de datos modificados |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| &nbsp; | Actualización gradual del grupo de disponibilidad |
| **Seguridad** | Administración extensible de claves |
| **Servicios de** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de SQL Server de 2017 RC1 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- El idioma predeterminado de la **sa** inicio de sesión es el inglés.

    - **Resolución**: cambiar el idioma de la **sa** inicio de sesión con la **ALTER LOGIN** instrucción.

#### <a name="databases"></a>Bases de datos

- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="remote-database-files"></a>Archivos de base de datos remota

- Hospedar los archivos de base de datos en un servidor NFS no se admite en esta versión. Esto incluye el uso de NFS para agrupación en clústeres, así como las bases de datos en instancias no clúster de conmutación por error de disco compartido. Estamos trabajando en habilitar la compatibilidad de servidor NFS en las próximas versiones.

#### <a name="cross-platform-availability-groups-and-distributed-availability-groups"></a>Grupos de disponibilidad de distintas plataformas y grupos de disponibilidad distribuidos

- Debido a un problema conocido, crear grupos de disponibilidad con réplicas en instancias hospedadas en Windows y Linux no funciona en esta versión. Esto incluye grupos de disponibilidad distribuidos. La corrección estará disponible en la próxima versión RC. 

#### <a name="server-collation"></a>Intercalación del servidor

- Al utilizar el MSSQL_COLLATION reemplazar o cuando se realiza una instalación localizada (no inglés), es posible SQL Server experimentarán un interbloqueo al intentar establecer la intercalación de servidor, lo que genera un volcado de memoria. El programa de instalación no completa correctamente, sin embargo no habrá se ha establecido la intercalación del servidor. La solución es volver a ejecutar. / conf mssql set-collation y escriba el nombre de intercalación deseado cuando se le solicite (el nombre de intercalación puede encontrarse en el registro de errores en la línea: "Intentando cambiar la intercalación predeterminada para..."). 
 
#### <a name="localization"></a>Localización

- Si no, la configuración regional es inglés (en_us) durante la instalación, debe usar la codificación UTF-8 en su sesión intensiva de errores/terminal. Si utiliza la codificación ASCII, verá un mensaje de error similar al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no puede utilizar la codificación UTF-8, ejecute el programa de instalación mediante la variable de entorno MSSQL_LCID para especificar la opción de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name = "fci"></a>Compartido actualización de instancia de clúster de disco

En RC1 el agente de recurso de clúster establece el nombre del servidor virtual como lo hace en una instancia de clúster de conmutación por error en Windows. Antes de RC1 `@@servername` en un disco compartido clúster devuelve el nodo específico, el nombre después de la conmutación por error `@@servername` devuelve un valor diferente. En RC1 el valor de serverName de la instancia de clúster de disco compartido se actualiza con el nombre de recurso cuando el recurso se agregará al clúster. Por este motivo, el clúster tendrá que reiniciar el servidor SQL Server después de la conmutación por error manual durante la actualización - como en los pasos siguientes:

1. Actualice primero el nodo secundario (pasivo) del clúster.
   - Actualizar **mssql server** paquete.
   - Actualizar **mssql-server-ha** paquete.
1. Conmutación por error manual al nodo actualizado.
   `pcs resource move <resourceName>`
   - Recurso produce un error inicialmente porque el agente de recursos comprueba el valor de serverName real y previsto. El valor de serverName esperado será diferente.
   - Clúster reiniciará el recurso de SQL Server en el mismo nodo. Esto actualizará el nombre del servidor.
1. Actualice el otro nodo. 
   - Actualizar **mssql server** paquete.
   - Actualizar **mssql-server-ha** paquete.
1. Quite la restricción agregada por el traslado de recursos manual. Vea [manualmente de clúster de conmutación por error](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md#failManual).
2. Si lo desea, producirá un error en el nodo principal original. 

#### <a name="availability-group"></a>grupo de disponibilidad

En Linux, no se admite la actualización de CTP de SQL Server de 2017 2.1 gradual a RC1. Después de actualizar la réplica secundaria, se desconectará de la réplica principal hasta que se actualiza la réplica principal. Microsoft está planeando resolver este problema en una versión futura.

#### <a name="full-text-search"></a>Búsqueda de texto completo
- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- El **mssql server es** paquete no es compatible con SUSE en esta versión. Se admite actualmente en Ubuntu y en Red Hat Enterprise Linux (RHEL).

- Las siguientes características no se admiten en esta versión, al ejecutar paquetes SSIS en Linux:
  - Base de datos de catálogo de SSIS
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - Ampliación SSIS
  - Feature Pack de Azure para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para obtener más información sobre SSIS en Linux, consulte los artículos siguientes:
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- Almacén de datos de administración (MDW) y el recopilador de datos en SSMS no son compatibles. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- No se puede modificar el número de archivos de registro que se va a conservar.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp21"></a>CTP 2.1 (mayo de 2017)
La versión del motor de SQL Server para esta versión es 14.0.600.250.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE]
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1 TB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. No es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.600.250-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.600.250-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.600.250-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.600.250-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.600.250-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.600.250-2_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.600.250-2_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools para Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (1.12) |

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de CTP de SQL Server de 2017 2.1 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- El idioma predeterminado de la **sa** inicio de sesión es el inglés.

    - **Resolución**: cambiar el idioma de la **sa** inicio de sesión con la **ALTER LOGIN** instrucción.

#### <a name="databases"></a>Bases de datos
- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="always-on-availability-group"></a>De grupo de disponibilidad AlwaysOn
- `sys.fn_hadr_backup_is_preffered_replica`no funciona para `CLUSTER_TYPE=NONE` o `CLUSTER_TYPE=EXTERNAL` porque se basa en el registro del clúster de WSFC con replicación de clave que no está disponible. Estamos trabajando en proporcionar una funcionalidad similar a través de una función diferente. 

#### <a name="full-text-search"></a>Búsqueda de texto completo
- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-agent"></a>Agente SQL
- Los siguientes componentes y subsistemas de trabajos del Agente SQL no se admiten actualmente en Linux:

    - Subsistemas: CmdExec, PowerShell, distribuidor de replicación, instantánea, mezcla, lectura de cola, SSIS, SSAS, SSRS
    - Alertas
    - Correo electrónico de base de datos
    - Agente de registro del LOG 
    - Captura de datos modificados

#### <a name="sqlpackage"></a>SqlPackage
- Mediante SqlPackage, debe especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/ tmp/sqlpackage. \<código \> /sistema/system32 "carpeta. 

  - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

#### <a name="ssis"></a> SQL Server Integration Services (SSIS)
Puede ejecutar paquetes SSIS en Linux. Para obtener más información, consulte el [blog post anunciar la compatibilidad con SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Tenga en cuenta los siguientes problemas conocidos con esta versión.

- El **mssql server es** paquete solo se admite en Ubuntu en este momento.

- Las siguientes características no se admiten al ejecutar paquetes SSIS en Linux:
  - Base de datos del catálogo SSIS
  - Programar la ejecución de paquetes del Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Controladores ODBC de terceros
  - Administrador de conexiones ODBC, origen y destino (compatible con SSIS en Linux CTP 2.1 Actualizar)
  - Captura de datos modificados (CDC)
  - Escalar horizontalmente
  - Feature Pack de Azure
  - Compatibilidad de Hadoop y HDFS
  - Microsoft Connector for SAP BW

Con SSIS en Linux CTP 2.1 actualizar, los paquetes SSIS pueden usar conexiones de ODBC en Linux. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- Almacén de datos de administración (MDW) y el recopilador de datos en SSMS no son compatibles. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- No se puede modificar el número de archivos de registro que se va a conservar.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp20"></a>En CTP 2.0 (abril de 2017)
La versión del motor de SQL Server para esta versión es 14.0.500.272.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS y 16,10 | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1 TB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.500.272-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.500.272-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.500.272-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |
| Paquete de Debian Ubuntu 16,10 | 14.0.500.272-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools para Visual Studio - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (0.2.1) |

> [!NOTE] 
> Las versiones de SQL Server Management Studio y SQL Server Data Tools especificadas anteriormente son candidatos de versión, por lo tanto, no se recomienda para su uso en producción.

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de SQL Server de 2017 CTP 2.0 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- El idioma predeterminado de la **sa** inicio de sesión es el inglés.

    - **Resolución**: cambiar el idioma de la **sa** inicio de sesión con la **ALTER LOGIN** instrucción.

#### <a name="databases"></a>Bases de datos
- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="always-on-availability-group"></a>De grupo de disponibilidad AlwaysOn
- Todas las configuraciones de alta disponibilidad - lo que significa que el grupo de disponibilidad se agrega como un recurso a un clúster marcapasos - creado con paquetes CTP2.0 anterior no son compatibles con versiones anteriores con el nuevo paquete. Eliminar todos los recursos clúster configurados previamente y crear nuevos grupos de disponibilidad con `CLUSTER_TYPE=EXTERNAL`. Vea [configurar de grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md).
- Grupos de disponibilidad que se crean con `CLUSTER_TYPE=NONE` y no se agregan como recursos en el clúster seguirá funcionando después de la actualización. Se usa para escenarios de escala de lectura. Vea [Configurar grupo de disponibilidad de la escala de lectura de SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md).
- `sys.fn_hadr_backup_is_preffered_replica`no funciona para `CLUSTER_TYPE=NONE` o `CLUSTER_TYPE=EXTERNAL` porque se basa en el registro del clúster de WSFC con replicación de clave que no está disponible. Estamos trabajando en proporcionar una funcionalidad similar a través de una función diferente. 

#### <a name="full-text-search"></a>Búsqueda de texto completo
- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

- El separador de palabras coreano tarda varios segundos en cargar y genera un error en el primer uso. Después de este error inicial, debería realizarse con normalidad.

#### <a name="sql-agent"></a>Agente SQL
- Los siguientes componentes y subsistemas de trabajos del Agente SQL no se admiten actualmente en Linux:

    - Subsistemas: CmdExec, PowerShell, distribuidor de replicación, instantánea, mezcla, lectura de cola, SSIS, SSAS, SSRS
    - Alertas
    - Correo electrónico de base de datos
    - Agente de registro del LOG 
    - Captura de datos modificados

#### <a name="sqlpackage"></a>SqlPackage
- Mediante SqlPackage, debe especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/ tmp/sqlpackage. \<código \> /sistema/system32 "carpeta. 

    - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- Almacén de datos de administración (MDW) y el recopilador de datos en SSMS no son compatibles. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- No se puede modificar el número de archivos de registro que se va a conservar.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp14"></a>CTP 1.4 (marzo de 2017)
La versión del motor de SQL Server para esta versión es 14.0.405.198.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS y 16,10 | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1 TB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las guías de instalación a continuación
-   [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
-   [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
-   [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.405.200-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.405.200-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.405.200-1 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |
| Paquete de Debian Ubuntu 16,10 | 14.0.405.200-1 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools para Visual Studio - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (0.2.1) |

> [!NOTE] 
> Las versiones de SQL Server Management Studio y SQL Server Data Tools especificadas anteriormente son candidatos de versión, por lo tanto, no se recomienda para su uso en producción.

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de SQL Server de 2017 CTP 1.4 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- No ejecute el comando `ALTER SERVICE MASTER KEY REGENERATE`. Hay un problema conocido que harán que SQL Server se vuelva inestable. Si necesita volver a generar la clave maestra de servicio, debe copia los archivos de base de datos, desinstalar y, a continuación, vuelva a instalar a SQL Server y, a continuación, restaurar los archivos de base de datos de nuevo más tarde.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Algunos nombres de zona horaria en Linux no se asignan exactamente a los nombres de zona horaria de Windows.

    - **Resolución**: Use nombres de zona horaria de la columna TZID de la ' asignación para: tabla de la sección de Windows en el [página de documentación de Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Motor de SQL Server espera que las líneas en los archivos de texto que debe finalizar con CR-LF (formato de línea de estilo de Windows).

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Todos los archivos de registro y los registros de errores están codificados en UTF-16.

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- **CREATE ASSEMBLY** no funcionará cuando intenta usar un archivo. Use la **FROM \<bits\> ** método en su lugar por ahora. 

#### <a name="databases"></a>Bases de datos
- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="always-on-availability-group"></a>De grupo de disponibilidad AlwaysOn
- Grupo de disponibilidad AlwaysOn recursos en clúster en Linux que se crearon con la versión 1.3 CTP se producirá un error después de actualizar el paquete HA (mssql-server-ha). 

   - **Resolución**: antes de actualizar el paquete de alta disponibilidad, establezca el parámetro de recurso de clúster `notify=true`. 
   
      - En el ejemplo siguiente se establece el parámetro de recurso de clúster en un recurso denominado **ag1** en RHEL o Ubuntu: 

      ```bash
      sudo pcs resource update ag1-master notify=true
      ```

      - Para SLES, actualizar la configuración de recurso de grupo de disponibilidad para agregar `notify=true`.  

      ```bash
      crm configure edit ms-ag_cluster 
      ```

      Agregar `notify=true` y guardar la configuración de recursos.

- Grupos de disponibilidad AlwaysOn en Linux puede estar sujeto a la pérdida de datos si réplicas están en modo de confirmación sincrónica. Ver detalles según corresponda para su distribución de Linux. 

   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES GRANDE](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

#### <a name="full-text-search"></a>Búsqueda de texto completo
- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

- El separador de palabras coreano tarda varios segundos en cargar y genera un error en el primer uso. Después de este error inicial, debería realizarse con normalidad.

#### <a name="sql-agent"></a>Agente SQL
- Los siguientes componentes y subsistemas de trabajos del Agente SQL no se admiten actualmente en Linux:
    - Subsistemas: CmdExec, PowerShell, distribuidor de replicación, instantánea, mezcla, lectura de cola, SSIS, SSAS, SSRS
    - Alertas
    - Correo electrónico de base de datos
    - Trasvase de registros
    - Agente de registro del LOG 
    - Captura de datos modificados

#### <a name="in-memory-oltp"></a>OLTP en memoria
- Solo se pueden crear bases de datos OLTP en memoria en el directorio /var/opt/mssql. Para obtener más información, visite la [tema de OLTP en memoria](sql-server-linux-performance-get-started.md#use-in-memory-oltp).

#### <a name="sqlpackage"></a>SqlPackage
- Mediante SqlPackage, debe especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/ tmp/sqlpackage. \<código \> /sistema/system32 "carpeta. 

    - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- No se admite el almacenamiento de datos de administración (MDW) y el recopilador de datos en SSMS. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- El Explorador de archivos se restringe a la "C:\\" ámbito, que se resuelve en/var/opt/mssql/en Linux. Para usar otras rutas de acceso, generar scripts de la operación de la interfaz de usuario y reemplace la unidad C:\\ rutas de acceso con las rutas de acceso de Linux. A continuación, ejecute el script manualmente en SSMS.

- No se puede modificar el número de archivos de registro que se va a conservar.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp13"></a>CTP 1.3 (febrero de 2017)
La versión del motor de SQL Server para esta versión es 14.0.304.138.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS y 16,10 | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1 TB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos descritos en la [guías de instalación](sql-server-linux-setup.md).

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.304.138-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[paquete MSSQL-server-ha RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[paquete de fts del servidor MSSQL RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.304.138-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[paquete MSSQL-server-ha RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[paquete de fts del servidor MSSQL RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.304.138-1 | [MSSQL server motor Debian de paquete](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[MSSQL-server-alta disponibilidad alta disponibilidad Debian paquete](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[paquete de Debian fts del servidor MSSQL búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |
| Paquete de Debian Ubuntu 16,10 | 14.0.304.138-1 | [MSSQL server motor Debian de paquete](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[MSSQL-server-alta disponibilidad alta disponibilidad Debian paquete](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[paquete de Debian fts del servidor MSSQL búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools para Visual Studio - Release Candidate 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (0.2.1) |

> [!NOTE] 
> Las versiones de SQL Server Management Studio y SQL Server Data Tools especificadas anteriormente son candidatos de versión, por lo tanto, no se recomienda para su uso en producción.

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | Agente SQL Server |
| &nbsp; | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de SQL Server de 2017 CTP 1.3 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- No ejecute el comando `ALTER SERVICE MASTER KEY REGENERATE`. Hay un problema conocido que harán que SQL Server se vuelva inestable. Si necesita volver a generar la clave maestra de servicio, debe copia los archivos de base de datos, desinstalar y, a continuación, vuelva a instalar a SQL Server y, a continuación, restaurar los archivos de base de datos de nuevo más tarde.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Algunos nombres de zona horaria en Linux no se asignan exactamente a los nombres de zona horaria de Windows.

    - **Resolución**: Use nombres de zona horaria de la columna TZID de la ' asignación para: tabla de la sección de Windows en el [página de documentación de Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Motor de SQL Server espera que las líneas en los archivos de texto que debe finalizar con CR-LF (formato de línea de estilo de Windows).

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Todos los archivos de registro y los registros de errores están codificados en UTF-16.

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- **CREATE ASSEMBLY** no funcionará cuando intenta usar un archivo. Use la **FROM \<bits\> ** método en su lugar por ahora. 

#### <a name="databases"></a>Bases de datos
- No se puede cambiar las ubicaciones de archivos de datos y de registro de TempDB.

- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

- Grupos de disponibilidad AlwaysOn en Linux puede estar sujeto a la pérdida de datos si réplicas están en modo de confirmación sincrónica. Vea 
 
   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES GRANDE](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   
#### <a name="full-text-search"></a>Búsqueda de texto completo
- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

- El separador de palabras coreano tarda varios segundos en cargar y genera un error en el primer uso. Después de este error inicial, debería realizarse con normalidad.

#### <a name="in-memory-oltp"></a>OLTP en memoria
- Solo se pueden crear bases de datos OLTP en memoria en el directorio /var/opt/mssql. Para obtener más información, visite la [tema de OLTP en memoria](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mediante SqlPackage, debe especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/tmp/sqlpackage./ <code/> /sistema/system32" carpeta. 

    - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

#### <a name="sqlcmdbcp--odbc"></a>SQLCMD y BCP y ODBC 
- Herramientas de línea de comandos de SQL Server (mssql-tools) y el controlador de ODBC (msodbcsql) depende de un administrador de controladores unixODBC personalizado. Esto hace que conflictos si tiene un administrador de controladores unixODBC instalado previamente. 

    - **Resolución**: en Ubuntu, el conflicto se resolverá automáticamente. Cuando se le pregunte si desea desinstalar el Administrador de controladores unixODBC existente, escriba 'y' y continuar con la instalación. En RedHat, tendrá que quitar manualmente el Administrador de controladores unixODBC existente mediante `yum remove unixODBC`. Estamos trabajando en solucionar esta limitación para RHEL y SUSE y debe tener una actualización para pronto.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- No se admite el almacenamiento de datos de administración (MDW) y el recopilador de datos en SSMS. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- El Agente SQL Server no se admite todavía. Por lo tanto, la funcionalidad de agente SQL Server en SSMS no funcionar en Linux en este momento.

- El Explorador de archivos se restringe a la "C:\\" ámbito, que se resuelve en/var/opt/mssql/en Linux. Para usar otras rutas de acceso, generar scripts de la operación de la interfaz de usuario y reemplace la unidad C:\\ rutas de acceso con las rutas de acceso de Linux. A continuación, ejecute el script manualmente en SSMS.

- No se puede modificar el número de archivos de registro que se va a conservar.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp12-ctp-12-january-2017"></a><a id="ctp12">CTP 1.2 (enero de 2017)
La versión del motor de SQL Server para esta versión es 14.0.200.24.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS y 16,10 | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server sólo ha sido probado hasta 256GB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos descritos en la [guías de instalación](sql-server-linux-setup.md).

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM | 14.0.200.24-2 | [paquete de server MSSQL 14.0.200.24-2 RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.200.24-2.x86_64.rpm)</br>[paquete de server MSSQL 14.0.200.24-2 RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.200.24-2.x86_64.rpm) | 
| Debian paquete | 14.0.200.24-2 | [paquete de server MSSQL 14.0.200.24-2 motor Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.200.24-2_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools para Visual Studio - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (0.2) |

> [!NOTE] 
> Las versiones de SQL Server Management Studio y SQL Server Data Tools especificadas anteriormente son candidatos de versión, por lo tanto, no se recomienda para su uso en producción.

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Búsqueda en texto completo |
| &nbsp; | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Grupos de disponibilidad AlwaysOn |
| &nbsp; | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | Agente SQL Server |
| &nbsp; | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de CTP de SQL Server de 2017 1.2 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- No ejecute el comando `ALTER SERVICE MASTER KEY REGENERATE`. Hay un problema conocido que harán que SQL Server se vuelva inestable. Si necesita volver a generar la clave maestra de servicio, debe copia los archivos de base de datos, desinstalar y, a continuación, vuelva a instalar a SQL Server y, a continuación, restaurar los archivos de base de datos de nuevo más tarde.

- Nombre del recurso para el recurso SQL ha cambiado de ocf:sql:fci a ocf:mssql:fci. Para obtener más información acerca de cómo configurar un clúster de conmutación por error de disco compartido puede encontrar [aquí](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure).

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Algunos nombres de zona horaria en Linux no se asignan exactamente a los nombres de zona horaria de Windows.

    - **Resolución**: Use nombres de zona horaria de la columna TZID de la ' asignación para: tabla de la sección de Windows en el [página de documentación de Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Motor de SQL Server espera que las líneas en los archivos de texto que debe finalizar con CR-LF (formato de línea de estilo de Windows).

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Todos los archivos de registro y los registros de errores están codificados en UTF-16.

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- **CREATE ASSEMBLY** no funcionará cuando intenta usar un archivo. Use la **FROM \<bits\> ** método en su lugar por ahora. 

#### <a name="databases"></a>Bases de datos
- No se puede cambiar las ubicaciones de archivos de datos y de registro de TempDB.

- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="in-memory-oltp"></a>OLTP en memoria
- Solo se pueden crear bases de datos OLTP en memoria en el directorio /var/opt/mssql. Estas bases de datos también deben tener el "C:\\" notación cuando se hace referencia. Para obtener más información, visite la [tema de OLTP en memoria](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mediante SqlPackage, debe especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/ tmp/sqlpackage. \<código \> /sistema/system32 "carpeta. 

    - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

#### <a name="sqlcmdbcp--odbc"></a>SQLCMD y BCP y ODBC 
- Si tiene una versión anterior de las herramientas de línea de comandos de SQL Server (mssql-herramientas) y el controlador de ODBC (msodbcsql), es posible que haya instalado un personalizada unixODBC (unixODBC-utf16) del Administrador de controladores. Esto podría provocar un posible conflicto como ya no se utiliza un administrador de controlador personalizado. 

    - **Resolución**: en Ubuntu y SLES, el conflicto se resolverá automáticamente. Cuando se le pregunte si desea desinstalar el Administrador de controladores unixODBC existente, escriba 'y' y continuar con la instalación. En RedHat, tendrá que quitar manualmente el Administrador de controladores unixODBC existente mediante `yum remove unixODBC-utf16 unixODBC-utf16-devel` y vuelva a intentar la instalación.
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- No se admite el almacenamiento de datos de administración (MDW) y el recopilador de datos en SSMS. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- El Agente SQL Server no se admite todavía. Por lo tanto, la funcionalidad de agente SQL Server en SSMS no funcionar en Linux en este momento.

- El Explorador de archivos se restringe a la "C:\\" ámbito, que se resuelve en/var/opt/mssql/en Linux. Para usar otras rutas de acceso, generar scripts de la operación de la interfaz de usuario y reemplace la unidad C:\\ rutas de acceso con las rutas de acceso de Linux. A continuación, ejecute el script manualmente en SSMS.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp11-ctp-11-december-2016"></a><a id="ctp11">CTP 1.1 (diciembre de 2016)
La versión del motor de SQL Server para esta versión es 14.0.100.187.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Estación de trabajo de Red Hat Enterprise Linux, de servidor y de escritorio | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS y 16,10 | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server sólo ha sido probado hasta 256GB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos descritos en la [guías de instalación](sql-server-linux-setup.md).

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM | 14.0.100.187-1 | [paquete de server MSSQL 14.0.100.187-1 RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.100.187-1.x86_64.rpm)</br>[paquete de server MSSQL 14.0.100.187-1 RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.100.187-1.x86_64.rpm) | 
| Debian paquete | 14.0.100.187-1 | [paquete de server MSSQL 14.0.100.187-1 motor Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.100.187-1_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools para Visual Studio - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (0.2) |

> [!NOTE] 
> Las versiones de SQL Server Management Studio y SQL Server Data Tools especificadas anteriormente son candidatos de versión, por lo tanto, no se recomienda para su uso en producción.

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Búsqueda en texto completo |
| &nbsp; | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Grupos de disponibilidad AlwaysOn |
| &nbsp; | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | Agente SQL Server |
| &nbsp; | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de CTP de SQL Server de 2017 1.1 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- No ejecute el comando `ALTER SERVICE MASTER KEY REGENERATE`. Hay un problema conocido que harán que SQL Server se vuelva inestable. Si necesita volver a generar la clave maestra de servicio, debe copia los archivos de base de datos, desinstalar y, a continuación, vuelva a instalar a SQL Server y, a continuación, restaurar los archivos de base de datos de nuevo más tarde.

- Nombre del recurso para el recurso SQL ha cambiado de ocf:sql:fci a ocf:mssql:fci. Para obtener más información acerca de cómo configurar un clúster de conmutación por error de disco compartido puede encontrar [aquí](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure).

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Algunos nombres de zona horaria en Linux no se asignan exactamente a los nombres de zona horaria de Windows.

    - **Resolución**: Use nombres de zona horaria de la columna TZID de la ' asignación para: tabla de la sección de Windows en el [página de documentación de Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Motor de SQL Server espera que las líneas en los archivos de texto que debe finalizar con CR-LF (formato de línea de estilo de Windows).

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Todos los archivos de registro y los registros de errores están codificados en UTF-16.

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- **CREATE ASSEMBLY** no funcionará cuando intenta usar un archivo. Use la **FROM \<bits\> ** método en su lugar por ahora. 

#### <a name="databases"></a>Bases de datos
- No se puede cambiar las ubicaciones de archivos de datos y de registro de TempDB.

- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="in-memory-oltp"></a>OLTP en memoria
- Solo se pueden crear bases de datos OLTP en memoria en el directorio /var/opt/mssql. Estas bases de datos también deben tener el "C:\" notación cuando se hace referencia. Para obtener más información, visite la [tema de OLTP en memoria](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Mediante SqlPackage, debe especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/ tmp/sqlpackage. \<código \> /sistema/system32 "carpeta. 

    - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

#### <a name="sqlcmdbcp--odbc"></a>SQLCMD y BCP y ODBC 
- Herramientas de línea de comandos de SQL Server (mssql-tools) y el controlador de ODBC (msodbcsql) depende de un administrador de controladores unixODBC personalizado. Esto hace que conflictos si tiene un administrador de controladores unixODBC instalado previamente. 

    - **Resolución**: en Ubuntu, el conflicto se resolverá automáticamente. Cuando se le pregunte si desea desinstalar el Administrador de controladores unixODBC existente, escriba 'y' y continuar con la instalación. En RedHat, tendrá que quitar manualmente el Administrador de controladores unixODBC existente mediante `yum remove unixODBC`. Estamos trabajando en solucionar esta limitación para RHEL y SUSE y debe tener una actualización para pronto.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- No se admite el almacenamiento de datos de administración (MDW) y el recopilador de datos en SSMS. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- El Agente SQL Server no se admite todavía. Por lo tanto, la funcionalidad de agente SQL Server en SSMS no funcionar en Linux en este momento.

- El Explorador de archivos se restringe a la "C:\\" ámbito, que se resuelve en/var/opt/mssql/en Linux. Para usar otras rutas de acceso, generar scripts de la operación de la interfaz de usuario y reemplace la unidad C:\\ rutas de acceso con las rutas de acceso de Linux. A continuación, ejecute el script manualmente en SSMS.

v

![Gráfico de barras de separación](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp10-ctp-10-november-2016"></a><a id="ctp10">CTP 1.0 (noviembre de 2016)
La versión del motor de SQL Server para esta versión es 14.0.1.246.

### <a name="supported-platforms"></a>Plataformas compatibles 

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.2 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS | EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server sólo ha sido probado hasta 256GB de memoria en este momento.

### <a name="package-details"></a>Detalles del paquete
En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos descritos en la [guías de instalación](sql-server-linux-setup.md).

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete RPM | 14.0.1.246-6 | [paquete de server MSSQL 14.0.1.246-6 RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.1.246-6.x86_64.rpm)</br>[paquete de server MSSQL 14.0.1.246-6 RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.1.246-6.x86_64.rpm) | 
| Debian paquete | 14.0.1.246-6 | [paquete de server MSSQL 14.0.1.246-6 motor Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.1.246-6_amd64.deb) |

### <a name="supported-client-tools"></a>Herramientas de cliente admitidos

| Herramienta | Versión mínima |
|-----|-----|
| [SQL Server Management Studio (SSMS) para Windows - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools para Visual Studio - Release Candidate 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Código de Visual Studio](https://code.visualstudio.com) con el [mssql extensión](https://aka.ms/mssql-marketplace) | Versión más reciente (0.1.5) |

> [!NOTE] 
> Las versiones de SQL Server Management Studio y SQL Server Data Tools especificadas anteriormente son candidatos de versión, por lo tanto, no se recomienda para su uso en producción.

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas
Las siguientes características y servicios no están disponibles en Linux en este momento. La compatibilidad de estas características se habilitarán cada vez más durante la cadencia mensual de actualizaciones del programa de vista previa.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Búsqueda en texto completo |
| &nbsp; | Replicación |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| **Alta disponibilidad** | Grupos de disponibilidad AlwaysOn |
| &nbsp; | Creación de reflejo de base de datos  |
| **Seguridad** | Autenticación de Active Directory |
| &nbsp; | Autenticación de Windows |
| &nbsp; | Administración extensible de claves |
| &nbsp; | Uso de certificado proporcionado por el usuario para SSL o TLS |
| **Servicios de** | Agente SQL Server |
| &nbsp; | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos
En las siguientes secciones se describen los problemas conocidos con esta versión de SQL Server de 2017 CTP1 en Linux.

#### <a name="general"></a>General
- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Algunos nombres de zona horaria en Linux no se asignan exactamente a los nombres de zona horaria de Windows.

    - **Resolución**: Use nombres de zona horaria de la columna TZID de la ' asignación para: tabla de la sección de Windows en el [página de documentación de Unicode.org](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html).

- Motor de SQL Server espera que las líneas en los archivos de texto que debe finalizar con CR-LF (formato de línea de estilo de Windows).

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Todos los archivos de registro y los registros de errores están codificados en UTF-16.

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- **CREATE ASSEMBLY** no funcionará cuando intenta usar un archivo. Use la **FROM \<bits\> ** método en su lugar por ahora.

#### <a name="databases"></a>Bases de datos
- No se puede cambiar las ubicaciones de archivos de datos y de registro de TempDB.

- No se puede mover las bases de datos del sistema con la utilidad mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten transacciones distribuidas.

#### <a name="in-memory-oltp"></a>OLTP en memoria
- Solo se pueden crear bases de datos OLTP en memoria en el directorio /var/opt/mssql. Estas bases de datos también deben tener el "C:\\" notación cuando se hace referencia. Para obtener más información, visite la [tema de OLTP en memoria](sql-server-linux-performance-get-started.md#use-in-memory-oltp).  

#### <a name="sqlpackage"></a>SqlPackage
- Uso de SqlPackage requiere para especificar una ruta de acceso absoluta para los archivos. Uso de rutas de acceso relativas se asignarán los archivos en el "/ tmp/sqlpackage. \<código \> /sistema/system32 "carpeta. 

    - **Resolución**: usar rutas de acceso absoluta del archivo.

- SqlPackage muestra la ubicación de archivos con un "C:\\" prefijo.

#### <a name="sqlcmdbcp--odbc"></a>SQLCMD y BCP y ODBC 
- Herramientas de línea de comandos de SQL Server (mssql-tools) y el controlador de ODBC (msodbcsql) depende de un administrador de controladores unixODBC personalizado. Esto hace que conflictos si tiene un administrador de controladores unixODBC instalado previamente. 

    - **Resolución**: en Ubuntu, el conflicto se resolverá automáticamente. Cuando se le pregunte si desea desinstalar el Administrador de controladores unixODBC existente, escriba 'y' y continuar con la instalación. En RedHat, tendrá que quitar manualmente el Administrador de controladores unixODBC existente mediante `yum remove unixODBC`. Estamos trabajando en solucionar esta limitación para RHEL y SUSE y debe tener una actualización para pronto.  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- No se admite el almacenamiento de datos de administración (MDW) y el recopilador de datos en SSMS. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- El Agente SQL Server no se admite todavía. Por lo tanto, la funcionalidad de agente SQL Server en SSMS no funcionar en Linux en este momento.

- El Explorador de archivos se restringe a la "C:\\" ámbito, que se resuelve en/var/opt/mssql/en Linux. Para usar otras rutas de acceso, generar scripts de la operación de la interfaz de usuario y reemplace la unidad C:\\ rutas de acceso con las rutas de acceso de Linux. A continuación, ejecute el script manualmente en SSMS.

### <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

