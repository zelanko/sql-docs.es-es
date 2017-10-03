---
title: "Notas de la versión de SQL Server 2017 en Linux | Documentos de Microsoft"
description: "Este tema contiene las notas de la versión y características admitidas en SQL Server 2017 ejecutando en Linux. Notas de la versión se incluyen con la versión más reciente y varias versiones anteriores."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: 7811cfe9238c92746673fac4fce40a4af44d6dcd
ms.openlocfilehash: 80c0813accf9f84204f057b9ef4efcad69142ec2
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de la versión de SQL Server 2017 en Linux

Las siguientes notas se aplican a SQL Server 2017 ejecutando en Linux. Esta versión admite muchas de las características del motor de base de datos de SQL Server para Linux. El siguiente tema se divide en secciones para cada versión, a partir de la ficha general más reciente versión de disponibilidad (GA) y las dos versiones anteriores. Ver la información en cada sección completa para las plataformas admitidas, herramientas, características y problemas conocidos.

En la tabla siguiente se enumera el historial de versiones de SQL Server 2017.

| Versión | Versión | Fecha de lanzamiento |
|-----|-----|-----|
| [GA](#GA) | 14.0.1000.169 | 10-2017 |
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| CTP 2.1 | 14.0.600.250 | 5-2017 |
| EN CTP 2.0 | 14.0.500.272 | 4-2017 |
| CTP 1.4 | 14.0.405.198 | 3-2017 |
| CTP 1.3 | 14.0.304.138 | 2-2017 |
| CTP 1.2 | 14.0.200.24 | 1-2017 |
| CTP 1.1 | 14.0.100.187 | 12-2016 |
| CTP 1.0 | 14.0.1.246 | 11-2016 |

## <a id="GA"></a>GA (octubre de 2017)

Se trata de la versión de la disponibilidad General (GA) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.1000.169.

### <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 o 7.4 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
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
| Paquete de Red Hat RPM | 14.0.1000.169-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.1000.169-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.1000.169-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

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
| &nbsp; | Autenticación de Active Directory para los servidores vinculados | 
| &nbsp; | Grupos de AD Authenticatin de disponibilidad (AG) | 
| **Servicios de** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>Problemas conocidos

En las siguientes secciones se describen los problemas conocidos con la versión de disponibilidad general (GA) de SQL Server 2017 en Linux.

#### <a name="general"></a>General

- Se admiten actualizaciones a la versión de GA de SQL Server 2017 de CTP 2.1 o superior. 

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

      ```bash
      sudo systemctl restart mssql-server
      ```

- No se puede restaurar las bases de datos de SQL Server 2014 en Windows que use OLTP en memoria en SQL Server 2017 en Linux. Para restaurar una base de datos de SQL Server 2014 que utiliza OLTP en memoria, actualizar las bases de datos a SQL Server 2016 o 2017 de SQL Server en Windows antes de pasar a SQL Server en Linux a través de copia de seguridad/restauración o separar y adjuntar.

- Permiso de usuario **ADMINISTER BULK OPERATIONS** no se admite en Linux en este momento.

#### <a name="networking"></a>Redes

Características que implican las conexiones TCP salientes desde el proceso sqlservr, como servidores vinculados o grupos de disponibilidad, podrían no funcionar si se cumplen las dos condiciones siguientes:

1. El servidor de destino se especifica como un nombre de host y no una dirección IP.

1. La instancia de origen tiene IPv6 deshabilitado en el kernel. Para comprobar que si el sistema tiene IPv6 habilitada en el kernel, deben pasar todas las pruebas siguientes:

   - `cat /proc/cmdline`se imprimirá el cmdline de arranque del núcleo actual. El resultado no debe contener `ipv6.disable=1`.
   - Sys/proc / / net/ipv6/directorio debe existir.
   - Un programa de C que llama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` debe ejecutarse correctamente: la syscall debe devolver un fd! = -1 y no producirá un error con EAFNOSUPPORT.

El error exacto depende de la característica. Para los servidores vinculados, esto se manifiesta como un error de tiempo de espera de inicio de sesión. Para los grupos de disponibilidad, el `ALTER AVAILABILITY GROUP JOIN` DDL en la base de datos secundaria se producirá un error después de 5 minutos con un error de tiempo de espera de configuración de descarga.

Para solucionar este problema, realice una de las siguientes acciones:

1. Usar direcciones IP en lugar de los nombres de host para especificar el destino de la conexión TCP.

1. Habilitar IPv6 en el kernel quitando `ipv6.disable=1` desde la línea de comandos de arranque. La manera de hacerlo depende de la distribución de Linux y el cargador de arranque, como grub. Si desea IPv6 que se deshabilite, todavía puede deshabilitar estableciendo `net.ipv6.conf.all.disable_ipv6 = 1` en el `sysctl` configuración (por ejemplo, `/etc/sysctl.conf`). Esto se sigue impedir que el adaptador de red del sistema entre una dirección IPv6, pero permitir que funcionen las características de sqlservr.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Si usa **Network File System (NFS)** recursos compartidos remotos en producción, tenga en cuenta los siguientes requisitos de soporte técnico:

- Utilice la versión NFS **4.2 o posterior**. Las versiones anteriores de NFS son compatibles con las características necesarias, como fallocate y la creación de archivos dispersos, comunes a sistemas de archivos modernos.
- Busque sólo el **/var/opt/mssql** directorios en el montaje NFS. No se admiten otros archivos, como los archivos binarios del sistema de SQL Server.
- Asegúrese de que los clientes NFS usan la opción 'nolock' al montar el recurso compartido remoto.

#### <a name="localization"></a>Localización

- Si no, la configuración regional es inglés (en_us) durante la instalación, debe usar la codificación UTF-8 en su sesión intensiva de errores/terminal. Si utiliza la codificación ASCII, verá un mensaje de error similar al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no puede utilizar la codificación UTF-8, ejecute el programa de instalación mediante la variable de entorno MSSQL_LCID para especificar la opción de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Cuando ejecuta el programa de instalación de mssql-conf y realizar una instalación distinta del inglés de SQL Server, incorrecto caracteres extendidos se muestran después del texto localizado, "Configuración de SQL Server …". O bien, para las instalaciones en función de no latinos, podría faltar la frase completamente. La frase que faltan debería mostrar la cadena adaptada siguiente: "el PID de licencia se procesó correctamente.  Es la nueva edición [<Name> edición] ". Esta cadena se genera solo para fines informativos y la actualización acumulativa del servidor SQL siguiente solucionará para todos los idiomas. Esto no afecta a la instalación correcta de SQL Server en modo alguno. 

#### <a name="full-text-search"></a>Búsqueda de texto completo

- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- El **mssql server es** paquete no es compatible con SUSE en esta versión. Se admite actualmente en Ubuntu y en Red Hat Enterprise Linux (RHEL).

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

Para obtener una lista de componentes SSIS integrados que no son compatibles actualmente o que son compatibles con limitaciones, vea [de extracción, transformación y carga datos en Linux con SSIS](sql-server-linux-migrate-ssis.md#components).

Para obtener más información sobre SSIS en Linux, consulte los artículos siguientes:
-   [Anuncio de entrada de blog compatibilidad con SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
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

### <a name="unsupported-features-and-services"></a>Servicios y características no admitidas

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
   
      ```bash
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

