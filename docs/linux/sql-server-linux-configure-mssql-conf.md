---
title: Configurar SQL Server en Linux | Documentos de Microsoft
description: "En este tema se describe cómo usar la herramienta mssql-conf para configurar SQL Server 2017 en Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 09/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.workload: On Demand
ms.openlocfilehash: 9aca5fe7905f06269bd07b7946c3bb6ef4e37492
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Configurar SQL Server en Linux con la herramienta mssql-conf

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

**MSSQL-conf** es un script de configuración que se instala con SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server y Ubuntu. Puede usar esta utilidad para establecer los parámetros siguientes:

|||
|---|---|
| [Intercalación](#collation) | Establecer una nueva intercalación de SQL Server en Linux. |
| [Comentarios de clientes](#customerfeedback) | Elija si SQL Server envía comentarios a Microsoft. |
| [Perfil de Correo electrónico de base de datos](#dbmail) | Establecer el perfil de correo electrónico de base de datos predeterminado de SQL Server en Linux |
| [Directorio de datos predeterminado](#datadir) | Cambie el directorio predeterminado para nuevos archivos de datos de base de datos de SQL Server (.mdf). |
| [Directorio de registro predeterminado](#datadir) | Cambia el directorio predeterminado para nuevos archivos de registro (.ldf) de base de datos de SQL Server. |
| [Directorio de volcado de memoria predeterminado](#dumpdir) | Cambie el directorio predeterminado para nuevos archivos de volcado de memoria y otros archivos de solución de problemas. |
| [Directorio de copia de seguridad predeterminado](#backupdir) | Cambiar el directorio predeterminado para los nuevos archivos de copia de seguridad. |
| [Tipo de volcado de memoria](#coredump) | Elija el tipo de archivo de volcado de memoria de volcado de memoria a recopilar. |
| [Alta disponibilidad](#hadr) | Habilite los grupos de disponibilidad. |
| [Directorio local de auditoría](#localaudit) | Establecer un directorio que desea agregar los archivos de auditoría Local. |
| [Configuración regional](#lcid) | Establecer la configuración regional para SQL Server que utilice. |
| [Límite de memoria](#memorylimit) | Establecer el límite de memoria para SQL Server. |
| [Puerto TCP](#tcpport) | Cambie el puerto que SQL Server escucha las conexiones. |
| [TLS](#tls) | Configurar la seguridad de nivel de transporte. |
| [TraceFlags](#traceflags) | Establecer el seguimiento que el servicio se va a usar. |

> [!TIP]
> Algunas de estas opciones también pueden configurarse con las variables de entorno. Para obtener más información, consulte [configuración configurar SQL Server con las variables de entorno](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Sugerencias de uso

* Para grupos de disponibilidad AlwaysOn y clústeres de discos compartidos, asegúrese siempre de los mismos cambios de configuración en cada nodo.

* Para el escenario de clúster de disco compartido, no intente reiniciar el **mssql server** servicio para aplicar los cambios. SQL Server se ejecuta como una aplicación. En su lugar, ponga el recurso sin conexión y, a continuación, vuelva a conectarse.

* Estos ejemplos ejecutar mssql-conf por especifican la ruta de acceso completa: **/opt/mssql/bin/mssql-conf**. Si elige navegar a esa ruta de acceso en su lugar, ejecute mssql-conf en el contexto del directorio actual: **. / conf mssql**.

## <a id="collation"></a>Cambiar la intercalación de SQL Server

El **conjunto intercalación** opción cambia el valor de intercalación a cualquiera de las intercalaciones admitidas.

1. Primera [las bases de datos de usuario de copia de seguridad](sql-server-linux-backup-and-restore-database.md) en el servidor.

1. A continuación, use la [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) procedimiento almacenado para separar las bases de datos de usuario.

1. Ejecute el **conjunto intercalación** opción y siga las indicaciones:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. La utilidad mssql-conf intentará cambiar el valor de intercalación especificada y reinicie el servicio. Si hay algún error, revierte la intercalación al valor anterior.

1. Restaurar las copias de seguridad de base de datos de usuario.

Para obtener una lista de intercalaciones admitidas, ejecute el [sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) función: `SELECT Name from sys.fn_helpcollations()`.

## <a id="customerfeedback"></a>Configurar los comentarios de clientes

El **telemetry.customerfeedback** cambios en la configuración si SQL Server envía comentarios a Microsoft o no. De forma predeterminada, este valor se establece en **true**. Para cambiar el valor, ejecute los siguientes comandos:

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.customerfeedback**. En el ejemplo siguiente se desactiva los comentarios de clientes mediante la especificación de **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obtener más información, consulte [comentarios de los clientes de SQL Server en Linux](sql-server-linux-customer-feedback.md).

## <a id="datadir"></a>Cambiar la ubicación del directorio de datos o de registro de forma predeterminada

El **filelocation.defaultdatadir** y **filelocation.defaultlogdir** configuración cambia la ubicación donde se crean los nuevos archivos de registro y base de datos. De forma predeterminada, esta ubicación es /var/opt/mssql/data. Para cambiar esta configuración, siga estos pasos:

1. Crear el directorio de destino para la nueva base de datos de archivos de registro y datos. En el ejemplo siguiente se crea un nuevo **/tmp/datos** directorio:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Cambiar el propietario y el grupo del directorio para la **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Utilice mssql-conf para cambiar el directorio de datos predeterminado con el **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Ahora se almacenarán todos los archivos de base de datos para las bases de datos creadas en esta nueva ubicación. Si desea cambiar la ubicación de los archivos de registro (.ldf) de las bases de datos, puede usar el comando "set" siguientes:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Este comando también se supone que existe un directorio de registro/tmp /, y que se encuentra en el usuario y grupo **mssql**.

## <a id="dumpdir"></a>Cambiar la ubicación predeterminada del directorio de volcado de memoria

El **filelocation.defaultdumpdir** cambios de configuración de la ubicación predeterminada donde se generan la memoria y los archivos de volcado SQL siempre que haya un bloqueo. De forma predeterminada, estos archivos se generan en /var/opt/mssql/log.

Para configurar esta nueva ubicación, use los siguientes comandos:

1. Crear el directorio de destino para los nuevos archivos de volcado de memoria. En el ejemplo siguiente se crea un nuevo **/tmp/dump** directorio:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. Cambiar el propietario y el grupo del directorio para la **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Utilice mssql-conf para cambiar el directorio de datos predeterminado con el **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="backupdir"></a>Cambiar la ubicación del directorio de copia de seguridad predeterminada

El **filelocation.defaultbackupdir** cambios de configuración de la ubicación predeterminada donde se generan los archivos de copia de seguridad. De forma predeterminada, estos archivos se generan en /var/opt/mssql/data.

Para configurar esta nueva ubicación, use los siguientes comandos:

1. Crear el directorio de destino para los nuevos archivos de copia de seguridad. En el ejemplo siguiente se crea un nuevo **copia deseguridad/tmp/** directory:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. Cambiar el propietario y el grupo del directorio para la **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. Use mssql-conf para cambiar el directorio de copia de seguridad predeterminado con el comando "set":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a>Especificar la configuración de volcado de memoria del núcleo

Si se produce una excepción en uno de los procesos de SQL Server, SQL Server crea un volcado de memoria.

Hay dos opciones para controlar el tipo de memoria volcados de memoria que SQL Server recopila: **coredump.coredumptype** y **coredump.captureminiandfull**. Estos se relacionan con las dos fases de la captura de volcado. 

La primera captura fase se controla mediante la **coredump.coredumptype** configuración, que determina el tipo de archivo de volcado de memoria generado durante una excepción. La segunda fase se habilita cuando la **coredump.captureminiandfull** configuración. Si **coredump.captureminiandfull** está establecido en true, el volcado de archivo especificado por **coredump.coredumptype** se genera y también se genera un minivolcado de segundo. Establecer **coredump.captureminiandfull** en false, se deshabilita la captura segundo intento.

1. Decida si desea capturar volcados minivolcados y completos con el **coredump.captureminiandfull** configuración.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Valor predeterminado: **false**

1. Especificar el tipo de archivo de volcado de memoria con el **coredump.coredumptype** configuración.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Valor predeterminado: **miniplus**

    En la tabla siguiente se enumera los posibles **coredump.coredumptype** valores.

    | Tipo | Description |
    |-----|-----|
    | **Mini** | Mini es el tipo de archivo de volcado de memoria más pequeño. Usa la información del sistema Linux para determinar los subprocesos y módulos en el proceso. El volcado de memoria contiene únicamente las pilas de subprocesos del entorno de host y los módulos. No contiene las referencias de memoria indirecta o variables globales. |
    | **miniplus** | MiniPlus es similar a mini, pero incluye memoria adicional. Entienda el funcionamiento interno de SQLPAL y el entorno de host, agregar las siguientes regiones de memoria para el volcado de memoria:</br></br> -Varias variables globales</br> -Toda la memoria por encima de 64TB</br> -Denominado se encontraron regiones en **$ / proc / pid/asignaciones**</br> -Memoria indirecta de subprocesos y las pilas</br> : Información del subproceso</br> -Asociado del Teb y del Peb</br> : Información del módulo</br> -Árbol VMM y VAD |
    | **filtrar** | Diseño de usos filtrado basado en resta donde se incluye toda la memoria en el proceso a menos que se excluyan específicamente. El diseño entiende el funcionamiento interno de SQLPAL y el entorno de host, excepto algunas regiones desde el volcado de memoria.
    | **completa** | Completa se encuentra un volcado de memoria de proceso completo que incluye todas las regiones en **/proc / $pid/asignaciones**. Esto no se controla mediante **coredump.captureminiandfull** configuración. |

## <a id="dbmail"></a>Establecer el perfil de correo electrónico de base de datos predeterminado de SQL Server en Linux

El **sqlpagent.databasemailprofile** permite establecer el perfil de correo electrónico de base de datos predeterminada para alertas por correo electrónico.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a>Alta disponibilidad

El **hadr.hadrenabled** opción permite a los grupos de disponibilidad en la instancia de SQL Server. El siguiente comando habilita grupos de disponibilidad estableciendo **hadr.hadrenabled** en 1. Debe reiniciar SQL Server para la configuración surta efecto.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Para obtener información de cómo se utiliza con grupos de disponibilidad, consulte los dos temas siguientes.

- [Configurar siempre en el grupo de disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)
- [Configurar grupo de disponibilidad de la escala de lectura para SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a>Directorio del conjunto de auditoría local

El **telemetry.userrequestedlocalauditdirectory** configuración habilita la auditoría Local y se crea permite establecer el directorio donde se registra la auditoría Local.

1. Cree un directorio de destino para los nuevos registros de auditoría Local. En el ejemplo siguiente se crea un nuevo **/tmp/auditoría** directorio:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Cambiar el propietario y el grupo del directorio para la **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obtener más información, consulte [comentarios de los clientes de SQL Server en Linux](sql-server-linux-customer-feedback.md).

## <a id="lcid"></a>Cambiar la configuración regional de SQL Server

El **language.lcid** cambios en la configuración la configuración regional de SQL Server a cualquier identificador de idioma admitidos (LCID). 

1. En el ejemplo siguiente se cambia la configuración regional en francés (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a>Establecer el límite de memoria

El **memory.memorylimitmb** opción controla la cantidad memoria física (en MB) disponible para SQL Server. El valor predeterminado es 80% de la memoria física.

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **memory.memorylimitmb**. En el ejemplo siguiente se cambia la memoria disponible para SQL Server a 3,25 GB (3328 MB).

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a>Cambiar el puerto TCP

El **network.tcpport** cambios en la configuración del puerto TCP donde SQL Server realiza escuchas para las conexiones. De forma predeterminada, este puerto se establece en 1433. Para cambiar el puerto, ejecute los siguientes comandos:

1. Ejecute el script mssql-conf como raíz con el comando "set" para "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Al conectarse a SQL Server, ahora, debe especificar el puerto personalizado con una coma (,) después del nombre de host o dirección IP. Por ejemplo, para conectar con SQLCMD, usaría el comando siguiente:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a>Especificar la configuración de TLS

Las siguientes opciones configura TLS para una instancia de SQL Server que se ejecutan en Linux.

|Opción |Description |
|--- |--- |
|**Network.forceencryption** |Si es 1, a continuación, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] obliga a todas las conexiones que se cifren. De forma predeterminada, esta opción es 0. |
|**Network.tlscert** |Archivo de la ruta de acceso absoluta para el certificado que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza para TLS. Ejemplo: `/etc/ssl/certs/mssql.pem` el archivo de certificado debe ser accesible para la cuenta de mssql. Microsoft recomienda restringir el acceso al archivo mediante `chown mssql:mssql <file>; chmod 400 <file>`. |
|**Network.tlskey** |Archivo de la ruta de acceso absoluta a la clave privada que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza para TLS. Ejemplo: `/etc/ssl/private/mssql.key` el archivo de certificado debe ser accesible para la cuenta de mssql. Microsoft recomienda restringir el acceso al archivo mediante `chown mssql:mssql <file>; chmod 400 <file>`. |
|**Network.tlsprotocols** |Una lista separada por comas de las TLS protocolos se admiten en SQL Server. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]siempre intenta negociar el protocolo permitido más fuerte. Si un cliente no es compatible con cualquier protocolo permitido, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rechazará el intento de conexión.  Para la compatibilidad, se permiten todos los protocolos admitidos de forma predeterminada (1.2, 1.1, 1.0).  Si los clientes admiten TLS 1.2, Microsoft recomienda que permite solo TLS 1.2. |
|**Network.tlsciphers** |Especifica los cifrados permitidos por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para TLS. Esta cadena debe tener el formato por [formato de lista de cifrado de OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). En general, no es necesario cambiar esta opción. <br /> De forma predeterminada, se permiten los cifrados siguientes: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **Network.kerberoskeytabfile** |Ruta de acceso al archivo de tabla de claves de Kerberos |

Para obtener un ejemplo del uso de la configuración de TLS, consulte [cifrar conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md).

## <a id="traceflags"></a>Habilitar/deshabilitar traceflags

Esto **marca de seguimiento** opción habilita o deshabilita el seguimiento para el inicio del servicio SQL Server. Para habilitar o deshabilitar una marca de seguimiento use los siguientes comandos:

1. Habilitar una marca de seguimiento con el comando siguiente. Por ejemplo, para 1234 de marca de seguimiento:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. Puede habilitar varios traceflags especificándolas por separado:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. De forma similar, puede deshabilitar uno o más traceflags habilitados especificarlos y agregando el **desactivar** parámetro:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Quitar una configuración

Para anular cualquier configuración realizada con `mssql-conf set`, llame a **mssql-conf** con el `unset` opción y el nombre de la configuración. Esto borra la configuración, de forma eficaz devolverlo a su valor predeterminado.

1. En el ejemplo siguiente se borran los **network.tcpport** opción.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Reinicie el servicio de SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Ver la configuración actual

Para ver cualquier configuración, ejecute el siguiente comando para generar el contenido de la **mssql.conf** archivo:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Tenga en cuenta que cualquier configuración que no se muestra en este archivo se utiliza sus valores predeterminados. La siguiente sección proporciona un ejemplo de **mssql.conf** archivo.

## <a name="mssqlconf-format"></a>formato de MSSQL.conf

El siguiente **/var/opt/mssql/mssql.conf** archivo proporciona un ejemplo para cada configuración. Puede usar este formato para realizar cambios manualmente para la **mssql.conf** archivo según sea necesario. Si cambia manualmente el archivo, debe reiniciar SQL Server antes de aplicarán los cambios. Para usar el **mssql.conf** archivo con Docker, debe tener Docker [conservar los datos](sql-server-linux-configure-docker.md). En primer lugar, agregue una completa **mssql.conf** de archivos en el directorio de host y, a continuación, ejecutar el contenedor. Hay un ejemplo de esto en [comentarios de los clientes](sql-server-linux-customer-feedback.md).

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

## <a name="next-steps"></a>Pasos siguientes

Para usar en su lugar, las variables de entorno para que algunos de estos cambios de configuración, consulte [configuración configurar SQL Server con las variables de entorno](sql-server-linux-configure-environment-variables.md).

Para otros escenarios y herramientas de administración, consulte [administrar SQL Server en Linux](sql-server-linux-management-overview.md).
