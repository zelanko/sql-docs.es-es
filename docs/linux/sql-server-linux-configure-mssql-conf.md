---
title: Configuración de SQL Server en Linux
description: En este artículo se describe cómo usar la herramienta mssql-conf para configurar la configuración de SQL Server en Linux.
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 57e43f3afd9c46e3b49e4f1f07ab3038359c8c50
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834007"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>Configurar SQL Server en Linux con la herramienta mssql-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**MSSQL-conf** es un script de configuración que se instala con SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server y Ubuntu. Puede usar esta utilidad para establecer los parámetros siguientes:

|||
|---|---|
| [Agente](#agent) | Habilitar el Agente SQL Server |
| [Intercalación](#collation) | Establecer una nueva intercalación de SQL Server en Linux. |
| [Comentarios del cliente](#customerfeedback) | Elija si SQL Server envía comentarios a Microsoft. |
| [Perfil de Correo electrónico de base de datos](#dbmail) | Establezca el perfil de correo electrónico de base de datos predeterminada para SQL Server en Linux. |
| [Directorio de datos predeterminado](#datadir) | Cambie el directorio predeterminado para nuevos archivos de datos de base de datos de SQL Server (.mdf). |
| [Directorio de registro predeterminado](#datadir) | Cambia el directorio predeterminado para nuevos archivos de registro (.ldf) de base de datos de SQL Server. |
| [Directorio predeterminado de la base de datos maestra](#masterdatabasedir) | Cambia el directorio predeterminado para los archivos de registro y base de datos maestra.|
| [Nombre de archivo de base de datos maestra predeterminada](#masterdatabasename) | Cambia el nombre de los archivos de base de datos maestra. |
| [Directorio de volcado de memoria predeterminado](#dumpdir) | Cambie el directorio predeterminado para nuevos volcados de memoria y otros archivos de solución de problemas. |
| [Directorio de registro de errores predeterminado](#errorlogdir) | Cambia el directorio predeterminado para nuevos archivos de registro de errores de SQL Server, seguimiento de Profiler de forma predeterminada, XE de sesión de estado del sistema y XE de sesión de Hekaton. |
| [Directorio de copia de seguridad predeterminado](#backupdir) | Cambiar el directorio predeterminado para los nuevos archivos de copia de seguridad. |
| [Tipo de volcado de memoria](#coredump) | Elija el tipo de archivo de volcado de memoria de volcado de memoria a recopilar. |
| [Alta disponibilidad](#hadr) | Habilite los grupos de disponibilidad. |
| [Directorio de auditoría local](#localaudit) | Establecer un directorio para agregar archivos de auditoría Local. |
| [Configuración regional](#lcid) | Establecer la configuración regional para SQL Server que utilice. |
| [Límite de memoria](#memorylimit) | Establecer el límite de memoria para SQL Server. |
| [Puerto TCP](#tcpport) | Cambiar el puerto donde escucha SQL Server para las conexiones. |
| [TLS](#tls) | Configurar la seguridad de nivel de transporte. |
| [Traceflags](#traceflags) | Establecer las marcas de seguimiento que se va a usar el servicio. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**MSSQL-conf** es un script de configuración que se instala con [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] para Red Hat Enterprise Linux, SUSE Linux Enterprise Server y Ubuntu. Puede usar esta utilidad para establecer los parámetros siguientes:

|||
|---|---|
| [Agente](#agent) | Habilitar el Agente SQL Server |
| [Intercalación](#collation) | Establecer una nueva intercalación de SQL Server en Linux. |
| [Comentarios del cliente](#customerfeedback) | Elija si SQL Server envía comentarios a Microsoft. |
| [Perfil de Correo electrónico de base de datos](#dbmail) | Establezca el perfil de correo electrónico de base de datos predeterminada para SQL Server en Linux. |
| [Directorio de datos predeterminado](#datadir) | Cambie el directorio predeterminado para nuevos archivos de datos de base de datos de SQL Server (.mdf). |
| [Directorio de registro predeterminado](#datadir) | Cambia el directorio predeterminado para nuevos archivos de registro (.ldf) de base de datos de SQL Server. |
| [Directorio de archivos de base de datos maestra predeterminado](#masterdatabasedir) | Cambia el directorio predeterminado para los archivos de base de datos maestra en la instalación de SQL existente.|
| [Nombre de archivo de base de datos maestra predeterminada](#masterdatabasename) | Cambia el nombre de los archivos de base de datos maestra. |
| [Directorio de volcado de memoria predeterminado](#dumpdir) | Cambie el directorio predeterminado para nuevos volcados de memoria y otros archivos de solución de problemas. |
| [Directorio de registro de errores predeterminado](#errorlogdir) | Cambia el directorio predeterminado para nuevos archivos de registro de errores de SQL Server, seguimiento de Profiler de forma predeterminada, XE de sesión de estado del sistema y XE de sesión de Hekaton. |
| [Directorio de copia de seguridad predeterminado](#backupdir) | Cambiar el directorio predeterminado para los nuevos archivos de copia de seguridad. |
| [Tipo de volcado de memoria](#coredump) | Elija el tipo de archivo de volcado de memoria de volcado de memoria a recopilar. |
| [Alta disponibilidad](#hadr) | Habilite los grupos de disponibilidad. |
| [Directorio de auditoría local](#localaudit) | Establecer un directorio para agregar archivos de auditoría Local. |
| [Configuración regional](#lcid) | Establecer la configuración regional para SQL Server que utilice. |
| [Límite de memoria](#memorylimit) | Establecer el límite de memoria para SQL Server. |
| [Coordinador de transacciones distribuidas de Microsoft](#msdtc) | Configurar y solucionar problemas de MSDTC en Linux. |
| [CLUF de MLServices](#mlservices-eula) | Aceptar R y Python CLUF para mlservices paquetes. Se aplica a SQL Server de 2019 únicamente.|
| [outboundnetworkaccess](#mlservices-outbound-access) |Habilitar el acceso de red saliente para [mlservices](sql-server-linux-setup-machine-learning.md) extensiones de R, Python y Java.|
| [Puerto TCP](#tcpport) | Cambiar el puerto donde escucha SQL Server para las conexiones. |
| [TLS](#tls) | Configurar la seguridad de nivel de transporte. |
| [Traceflags](#traceflags) | Establecer las marcas de seguimiento que se va a usar el servicio. |

::: moniker-end

> [!TIP]
> Algunas de estas opciones también pueden configurarse con variables de entorno. Para obtener más información, consulte [opciones de configuración de SQL Server con variables de entorno](sql-server-linux-configure-environment-variables.md).

## <a name="usage-tips"></a>Sugerencias de uso

* Para grupos de disponibilidad AlwaysOn y clústeres de discos compartidos, realizar siempre los mismos cambios de configuración en cada nodo.

* Para el escenario de clúster de disco compartido, no intente reiniciar el **mssql-server** servicio para aplicar los cambios. SQL Server se ejecuta como una aplicación. En su lugar, poner el recurso sin conexión y, a continuación, vuelva a conectarse.

* Estos ejemplos ejecutan mssql-conf especificando la ruta de acceso completa: **/opt/mssql/bin/mssql-conf**. Si opta por desplazarse a esa ruta de acceso en su lugar, ejecute mssql-conf en el contexto del directorio actual: **. / mssql-conf**.

## <a id="agent"></a> Habilitar el Agente SQL Server

El **sqlagent.enabled** configuración permite [del Agente SQL Server](sql-server-linux-run-sql-server-agent-job.md). De forma predeterminada, el Agente SQL Server está deshabilitado. Si **sqlagent.enabled** no está presente en el archivo de configuración mssql.conf, a continuación, SQL Server internamente se da por supuesto que el Agente SQL Server está deshabilitado.

Para cambiar esta configuración, siga estos pasos:

1. Habilitar al Agente SQL Server:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> Cambiar la intercalación de SQL Server

El **conjunto intercalación** opción cambia el valor de intercalación a cualquiera de las intercalaciones admitidas.

1. Primera [las bases de datos de usuario de copia de seguridad](sql-server-linux-backup-and-restore-database.md) en el servidor.

1. A continuación, utilice el [sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) procedimiento almacenado para separar las bases de datos de usuario.

1. Ejecute el **conjunto intercalación** opción y siga las indicaciones:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. La utilidad mssql-conf intentará cambiar el valor de la intercalación especificada y reinicie el servicio. Si hay algún error, revierte la intercalación al valor anterior.

1. Restaure las copias de seguridad de base de datos de usuario.

Para obtener una lista de intercalaciones admitidas, ejecute el [sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) función: `SELECT Name from sys.fn_helpcollations()`.

## <a id="customerfeedback"></a> Configurar los comentarios de clientes

El **telemetry.customerfeedback** cambios de configuración si SQL Server envía comentarios a Microsoft o no. De forma predeterminada, este valor se establece en **true** para todas las ediciones. Para cambiar el valor, ejecute los siguientes comandos:

> [!IMPORTANT]
> Puede no desactivar los comentarios de clientes de forma gratuita las ediciones de SQL Server, Express y Developer.

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.customerfeedback**. En el ejemplo siguiente se desactiva los comentarios de clientes mediante la especificación de **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

Para obtener más información, consulte [comentarios del cliente para SQL Server en Linux](sql-server-linux-customer-feedback.md) y [declaración de privacidad de SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a id="datadir"></a> Cambiar la ubicación del directorio de datos o de registro de forma predeterminada

El **filelocation.defaultdatadir** y **filelocation.defaultlogdir** configuración cambia la ubicación donde se crean los nuevos archivos de registro y base de datos. De forma predeterminada, esta ubicación es /var/opt/mssql/data. Para cambiar esta configuración, use los pasos siguientes:

1. Cree el directorio de destino para la nueva base de datos de archivos de registro y datos. En el ejemplo siguiente se crea un nuevo **/tmp/datos** directorio:

   ```bash
   sudo mkdir /tmp/data
   ```

1. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. Use mssql-conf para cambiar el directorio de datos de forma predeterminada con la **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

1. Ahora todos los archivos de base de datos para las bases de datos nuevas creadas se almacenarán en esta nueva ubicación. Si desea cambiar la ubicación de los archivos de registro (.ldf) de las bases de datos, puede usar el comando "set" siguientes:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. Este comando también se supone que existe un directorio de registro/tmp /, y que se encuentra en el usuario y grupo **mssql**.


## <a id="masterdatabasedir"></a> Cambiar la ubicación de directorio del archivo de base de datos maestra predeterminada

El **filelocation.masterdatafile** y **filelocation.masterlogfile** cambios de configuración de la ubicación donde el motor de SQL Server busca los archivos de base de datos maestra. De forma predeterminada, esta ubicación es /var/opt/mssql/data.

Para cambiar esta configuración, use los pasos siguientes:

1. Crear el directorio de destino para los nuevos archivos de registro de error. En el ejemplo siguiente se crea un nuevo **/tmp/masterdatabasedir** directorio:

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. Usar mssql-conf para cambiar el directorio de la base de datos maestra predeterminada para los archivos de registro y de datos maestra con el **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > Además de mover los archivos de registro y datos maestros, también se mueve la ubicación predeterminada para todas las demás bases de datos del sistema.

1. Detenga el servicio de SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Mover el master.mdf y masterlog.ldf:

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. Inicie el servicio de SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > Si SQL Server no encuentra los archivos master.mdf y mastlog.ldf en el directorio especificado, se crearán automáticamente una copia de las bases de datos del sistema con plantilla en el directorio especificado y se iniciará correctamente SQL Server. Sin embargo, los metadatos, como las bases de datos de usuario, los inicios de sesión de servidor, los certificados de servidor, las claves de cifrado, trabajos del Agente SQL o antigua contraseña de inicio de sesión de SA no se actualizará en la nueva base de datos maestra. Tendrá que detener SQL Server y mover los antiguos master.mdf y mastlog.ldf a la nueva ubicación especificada e inicie SQL Server para continuar usando los metadatos existentes.
 
## <a id="masterdatabasename"></a> Cambiar el nombre de los archivos de base de datos maestra

El **filelocation.masterdatafile** y **filelocation.masterlogfile** cambios de configuración de la ubicación donde el motor de SQL Server busca los archivos de base de datos maestra. También puede usar para cambiar el nombre de los archivos de registro y base de datos maestra. 

Para cambiar esta configuración, use los pasos siguientes:

1. Detenga el servicio de SQL Server:

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Use mssql-conf para cambiar los nombres de base de datos maestra esperado para los archivos de registro y de datos maestra con el **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > Solo puede cambiar el nombre de la base de datos maestra y los archivos de registro después de que SQL Server se ha iniciado correctamente. Antes de la ejecución inicial, SQL Server espera que los archivos se denomine master.mdf y mastlog.ldf.

1. Cambiar el nombre de los archivos de datos y registro de base de datos maestra 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. Inicie el servicio de SQL Server:

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> Cambiar la ubicación predeterminada del directorio de volcado de memoria

El **filelocation.defaultdumpdir** cambios de configuración de la ubicación predeterminada donde se generan la memoria y volcados de memoria SQL siempre que haya un bloqueo. De forma predeterminada, estos archivos se generan en /var/opt/mssql/log.

Para configurar esta nueva ubicación, use los siguientes comandos:

1. Cree el directorio de destino para los nuevos archivos de volcado de memoria. En el ejemplo siguiente se crea un nuevo **/tmp/dump** directorio:

   ```bash
   sudo mkdir /tmp/dump
   ```

1. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. Use mssql-conf para cambiar el directorio de datos de forma predeterminada con la **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> Cambiar la ubicación de directorio predeterminada archivo de registro de error

El **filelocation.errorlogfile** cambios de configuración de la ubicación donde se crean el nuevo registro de errores, seguimiento de profiler de forma predeterminada, sesión XE de mantenimiento del sistema y archivos de sesión de XE de Hekaton. De forma predeterminada, esta ubicación es /var/opt/mssql/log. El directorio en el que se establece el archivo de registro de errores SQL se convierte en el directorio de registro predeterminado para otros registros.

Para cambiar esta configuración:

1. Crear el directorio de destino para los nuevos archivos de registro de error. En el ejemplo siguiente se crea un nuevo **/tmp/logs** directorio:

   ```bash
   sudo mkdir /tmp/logs
   ```

1. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. Use mssql-conf para cambiar el nombre de archivo de registro de errores de forma predeterminada con la **establecer** comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> Cambiar la ubicación del directorio de copia de seguridad predeterminada

El **filelocation.defaultbackupdir** cambios de configuración de la ubicación predeterminada donde se generan los archivos de copia de seguridad. De forma predeterminada, estos archivos se generan en /var/opt/mssql/data.

Para configurar esta nueva ubicación, use los siguientes comandos:

1. Cree el directorio de destino para los nuevos archivos de copia de seguridad. En el ejemplo siguiente se crea un nuevo **/tmp/backup** directorio:

   ```bash
   sudo mkdir /tmp/backup
   ```

1. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

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

## <a id="coredump"></a> Especificar la configuración de volcado de núcleo

Si se produce una excepción en uno de los procesos de SQL Server, SQL Server crea un volcado de memoria.

Hay dos opciones para controlar el tipo de memoria volcados de memoria que SQL Server recopila: **coredump.coredumptype** y **coredump.captureminiandfull**. Estos se refieren a las dos fases de la captura de volcado de núcleo. 

La primera captura de fase se controla mediante el **coredump.coredumptype** configuración, que determina el tipo de archivo de volcado generado durante una excepción. La segunda fase se habilita cuando la **coredump.captureminiandfull** configuración. Si **coredump.captureminiandfull** se establece en true, el volcado de archivo especificado por **coredump.coredumptype** se genera y también se genera un minivolcado de segundo. Establecer **coredump.captureminiandfull** en false, se deshabilita la captura del segundo intento.

1. Decida si desea capturar volcados minivolcados y completos con el **coredump.captureminiandfull** configuración.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    Valor predeterminado: **false**

1. Especifique el tipo de archivo de volcado de memoria con el **coredump.coredumptype** configuración.

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    Valor predeterminado: **miniplus**

    En la tabla siguiente se enumera los posibles **coredump.coredumptype** valores.

    | Type | Descripción |
    |-----|-----|
    | **mini** | Mini es el tipo de archivo de volcado de memoria más pequeño. La información del sistema Linux usa para determinar los subprocesos y módulos en el proceso. El volcado de memoria contiene solo los módulos y las pilas de subprocesos del entorno de host. No tiene referencias de memoria indirecta o variables globales. |
    | **miniplus** | Es similar a mini miniPlus, pero incluye memoria adicional. Comprende los aspectos internos de SQLPAL y el entorno de host, agregar las siguientes regiones de memoria para el volcado de memoria:</br></br> -Globals varios</br> -Toda la memoria por encima de 64TB</br> -Denominado regiones se encuentra en   **/proc / pid de $/ asignaciones**</br> -Memoria indirecta de subprocesos y las pilas</br> : La información de subproceso</br> -Asociada del Teb y del Peb</br> : Información de módulo</br> -VMM y VAD árbol |
    | **filtered** | Diseño de usos filtrado basado en una resta donde se incluye toda la memoria en el proceso a menos que se excluyan específicamente. El diseño comprende los aspectos internos de SQLPAL y el entorno de host, exclusión de determinadas regiones del volcado de memoria.
    | **full** | Completa se encuentra un volcado de memoria de proceso completo que incluye todas las regiones en **/proc / pid de $/ asignaciones**. Esto no se controla mediante **coredump.captureminiandfull** configuración. |

## <a id="dbmail"></a> Establecer el perfil de correo electrónico de base de datos predeterminada de SQL Server en Linux

El **sqlpagent.databasemailprofile** le permite establecer el perfil de correo electrónico de base de datos predeterminada para alertas por correo electrónico.

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> Alta disponibilidad

El **hadr.hadrenabled** opción permite a los grupos de disponibilidad en la instancia de SQL Server. El siguiente comando habilita grupos de disponibilidad estableciendo **hadr.hadrenabled** en 1. Debe reiniciar SQL Server para la configuración surta efecto.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

Para obtener información sobre cómo se utiliza con grupos de disponibilidad, consulte los dos temas siguientes.

- [Configurar siempre en el grupo de disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)
- [Configurar el grupo de disponibilidad de escalado de lectura para SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> Directorio del conjunto de auditoría local

El **telemetry.userrequestedlocalauditdirectory** configuración habilita la auditoría Local y permite establecer el directorio de registros de auditoría Local donde se crea.

1. Cree un directorio de destino para los nuevos registros de auditoría Local. En el ejemplo siguiente se crea un nuevo **/tmp/auditoría** directorio:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

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

Para obtener más información, consulte [comentarios del cliente para SQL Server en Linux](sql-server-linux-customer-feedback.md).

## <a id="lcid"></a> Cambiar la configuración regional de SQL Server

El **language.lcid** establecer cambia la configuración regional de SQL Server a cualquier identificador de idioma admitidos (LCID). 

1. En el ejemplo siguiente se cambia la configuración regional en francés (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> Establecer el límite de memoria

El **memory.memorylimitmb** opción controla la cantidad memoria física (en MB) disponible para SQL Server. El valor predeterminado es 80% de la memoria física.

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **memory.memorylimitmb**. El ejemplo siguiente cambia la memoria disponible para SQL Server a 3,25 GB (3328 MB).

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> Configurar MSDTC

El **network.rpcport** y **distributedtransaction.servertcpport** configuración se utiliza para configurar el Coordinador de transacciones distribuidas de Microsoft (MSDTC). Para cambiar esta configuración, ejecute los siguientes comandos:

1. Ejecute el script mssql-conf como raíz con el **establecer** el comando para "network.rpcport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. A continuación, establezca la configuración de "distributedtransaction.servertcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

Además de establecer estos valores, también debe configurar el enrutamiento y actualizar el firewall para el puerto 135. Para obtener más información sobre cómo hacerlo, consulte [cómo configurar MSDTC en Linux](sql-server-linux-configure-msdtc.md).

Hay otras opciones para mssql-conf que puede usar para supervisar y solucionar problemas de MSDTC. La siguiente tabla describe brevemente estos valores. Para obtener más información sobre su uso, consulte los detalles en el artículo de soporte técnico de Windows, [cómo habilitar el seguimiento de diagnóstico de MS DTC](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute).

| mssql-conf setting | Descripción |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | Configurar llamadas RPC sola seguras para las transacciones distribuidas |
| distributedtransaction.fallbacktounsecurerpcifnecessary | Configurar llamadas RPC sola de seguridad para distribuir |transacciones
| distributedtransaction.maxlogsize | Tamaño de archivo del registro de transacciones DTC en MB. El valor predeterminado es 64MB |
| distributedtransaction.memorybuffersize | Tamaño del búfer circular en el que se almacenan los seguimientos. Este tamaño en MB y el valor predeterminado es 10MB |
| distributedtransaction.servertcpport | Puerto del servidor de rpc MSDTC |
| distributedtransaction.trace_cm | Seguimientos en el Administrador de conexiones |
| distributedtransaction.trace_contact | Realiza un seguimiento de los contactos y el grupo de contactos |
| distributedtransaction.trace_gateway | Origen de la puerta de enlace de seguimientos |
| distributedtransaction.trace_log | Seguimiento de registro |
| distributedtransaction.trace_misc | Seguimientos que no se pueden dividir en las otras categorías |
| distributedtransaction.trace_proxy | Seguimientos que se generan en el proxy MSDTC |
| distributedtransaction.trace_svc | Realiza un seguimiento de servicio y .exe del inicio del archivo |
| distributedtransaction.trace_trace | La infraestructura de seguimiento propio |
| distributedtransaction.trace_util | Realiza un seguimiento de las rutinas de utilidad que se llaman desde varias ubicaciones |
| distributedtransaction.trace_xa | Origen de seguimiento del Administrador de transacciones XA (XATM) |
| distributedtransaction.tracefilepath | Carpeta de seguimiento que se deben almacenar los archivos |
| distributedtransaction.turnoffrpcsecurity | Habilitar o deshabilitar la seguridad RPC para las transacciones distribuidas |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> Acepte el CLUF MLServices

Agregar [paquetes de R o Python de aprendizaje automático](sql-server-linux-setup-machine-learning.md) a la base de datos motor requiere que acepte los términos de licencia para las distribuciones de código abierto de R y Python. En la tabla siguiente enumera todos los comandos disponibles o las opciones relacionadas con mlservices CLUF. Se usa el mismo parámetro de términos de licencia de R y Python, según lo que haya instalado.

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

También puede agregar directamente a la aceptación del CLUF del [mssql.conf archivo](#mssql-conf-format):

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-outbound-access"></a> Habilitar el acceso de red saliente

Acceso de red saliente para las extensiones de Java, Python y R en el [SQL Server Machine Learning Services](sql-server-linux-setup-machine-learning.md) característica está deshabilitada de forma predeterminada. Para habilitar las solicitudes salientes, establezca el "outboundnetworkaccess" propiedad Boolean mediante mssql-conf.

Después de establecer la propiedad, reinicie el servicio Launchpad de SQL Server para leer los valores actualizados en el archivo INI. Un mensaje de reinicio le recuerda que cada vez que se modifica una configuración de extensibilidad.

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
/opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

También puede agregar "outboundnetworkaccess" directamente a la [mssql.conf archivo](#mssql-conf-format):

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a id="tcpport"></a> Cambiar el puerto TCP

El **network.tcpport** el puerto TCP donde escucha SQL Server para las conexiones de cambios de configuración. De forma predeterminada, este puerto se establece en 1433. Para cambiar el puerto, ejecute los siguientes comandos:

1. Ejecute el script mssql-conf como raíz con el comando "set" para "network.tcpport":

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```

3. Al conectarse a SQL Server, ahora, debe especificar el puerto personalizado con una coma (,) después de la dirección IP o nombre de host. Por ejemplo, para conectarse con SQLCMD, usaría el siguiente comando:

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> Especificar la configuración de TLS

Las siguientes opciones de configuración TLS para una instancia de SQL Server que se ejecutan en Linux.

|Opción |Descripción |
|--- |--- |
|**network.forceencryption** |Si es 1, a continuación, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] obliga a todas las conexiones a cifrarse. De forma predeterminada, esta opción es 0. |
|**network.tlscert** |Archivo de la ruta de acceso absoluta para el certificado que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa TLS. Ejemplo:   `/etc/ssl/certs/mssql.pem`  El archivo de certificado debe ser accesible para la cuenta de mssql. Microsoft recomienda restringir el acceso al archivo mediante `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlskey** |Archivo de la ruta de acceso absoluta a la clave privada que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa TLS. Ejemplo:  `/etc/ssl/private/mssql.key`  El archivo de certificado debe ser accesible para la cuenta de mssql. Microsoft recomienda restringir el acceso al archivo mediante `chown mssql:mssql <file>; chmod 400 <file>`. |
|**network.tlsprotocols** |Una lista separada por comas de qué TLS protocolos se admiten en SQL Server. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] siempre intenta negociar el protocolo permitido más fuerte. Si un cliente no es compatible con cualquier protocolo permitido, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] rechazará el intento de conexión.  Para la compatibilidad, se permiten todos los protocolos admitidos de forma predeterminada (1.2, 1.1, 1.0).  Si los clientes admiten TLS 1.2, Microsoft recomienda que permite solo TLS 1.2. |
|**network.tlsciphers** |Especifica los cifrados que están permitidos por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para TLS. Esta cadena debe tener el formato por [formato de lista de cifrado de OpenSSL](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html). En general, no es necesario cambiar esta opción. <br /> De forma predeterminada, se permiten los cifrados siguientes: <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Ruta de acceso al archivo keytab de Kerberos |

Para obtener un ejemplo del uso de la configuración de TLS, consulte [cifrar conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md).

## <a id="traceflags"></a> Habilitar o deshabilitar marcas de seguimiento

Esto **la marca de seguimiento** opción habilita o deshabilita las marcas de seguimiento para el inicio del servicio SQL Server. Para habilitar o deshabilitar una marca de seguimiento use los siguientes comandos:

1. Habilitar una marca de seguimiento con el comando siguiente. Por ejemplo, para la marca de seguimiento 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. Puede habilitar varias marcas de seguimiento mediante la especificación de ellos por separado:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. De forma similar, puede deshabilitar uno o más marcas de seguimiento habilitadas especificarlos y agregando el **desactivar** parámetro:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>Quitar una configuración

Para anular cualquier configuración realizada con `mssql-conf set`, llame a **mssql-conf** con el `unset` opción y el nombre de la configuración. Esto borra la configuración, eficazmente devolverlo a su valor predeterminado.

1. El siguiente ejemplo se borra el **network.tcpport** opción.

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. Reinicie el servicio de SQL Server.

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>Ver la configuración actual

Para ver cualquier configurado, ejecute el siguiente comando para generar el contenido de la **mssql.conf** archivo:

```bash
sudo cat /var/opt/mssql/mssql.conf
```

Tenga en cuenta que cualquier configuración que no se muestra en este archivo usa sus valores predeterminados. La siguiente sección proporciona un ejemplo **mssql.conf** archivo.


## <a id="mssql-conf-format"></a> mssql.conf format

La siguiente **/var/opt/mssql/mssql.conf** archivo proporciona un ejemplo para cada configuración. Puede usar este formato para realizar manualmente los cambios realizados en el **mssql.conf** archivo según sea necesario. Si cambia manualmente el archivo, debe reiniciar SQL Server antes de aplicarán los cambios. Para usar el **mssql.conf** archivo con Docker, debe tener Docker [conservar los datos](sql-server-linux-configure-docker.md). En primer lugar, agregue una completa **mssql.conf** de archivos a su directorio de host y, a continuación, ejecute el contenedor. Hay un ejemplo de esto en [comentarios de los clientes](sql-server-linux-customer-feedback.md).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

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

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

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
rpcport = 13500
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

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para usar en su lugar, las variables de entorno para agregar algunos de estos cambios de configuración, consulte [opciones de configuración de SQL Server con variables de entorno](sql-server-linux-configure-environment-variables.md).

Para otros escenarios y las herramientas de administración, consulte [administrar SQL Server en Linux](sql-server-linux-management-overview.md).
