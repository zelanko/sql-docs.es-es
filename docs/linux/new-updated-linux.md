---
title: 'Actualizado: SQL Server en documentos de Linux | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Microsoft SQL Server en Linux."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 9e6b139e45ccb5184255eabedfb0f809ff64fd2b
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Las nuevas y recientemente actualizado: SQL Server en documentos de Linux



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-07-18** &nbsp; - a - &nbsp; **2017-09-11**
- *Área de asunto:* &nbsp; **Microsoft SQL Server en Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Correo electrónico de base de datos y las alertas de correo electrónico con el Agente SQL en Linux](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que se han producido recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección de citas.

1. [Funcionar el grupo de disponibilidad de alta disponibilidad para SQL Server en Linux](#TitleNum_1)
2. [Configurar SQL Server 2017 imágenes del contenedor en Docker](#TitleNum_2)
3. [Configurar SQL Server en Linux con la herramienta mssql-conf](#TitleNum_3)
4. [Comentarios de los clientes de SQL Server en Linux](#TitleNum_4)
5. [Migrar una base de datos de SQL Server de Windows para Linux con backup y restore](#TitleNum_5)
6. [Notas de la versión de SQL Server 2017 en Linux](#TitleNum_6)
7. [Guía de instalación para SQL Server en Linux](#TitleNum_7)
8. [Instalar SQL Server Integration Services (SSIS) en Linux](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-operate-ha-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-failover-hamd"></a>1. &nbsp;[Grupo funcionar HA de disponibilidad de SQL Server en Linux](sql-server-linux-availability-group-failover-ha.md)

*Actualizado: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**Actualizar grupo de disponibilidad**


Antes de actualizar un grupo de disponibilidad, revise las prácticas recomendadas en [actualización disponibilidad grupo réplica instancias--.. / database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

Las siguientes secciones explican cómo realizar una actualización gradual con instancias de SQL Server en Linux con grupos de disponibilidad.

**Pasos de actualización en Linux**


Una vez réplicas del grupo de disponibilidad en las instancias de SQL Server en Linux, el tipo de clúster del grupo de disponibilidad es `EXTERNAL` o `NONE`. Un grupo de disponibilidad que está administrado por un administrador de clústeres, además de clúster de conmutación por error de Windows Server (WSFC) es `EXTERNAL`. Marcapasos con Corosync es un ejemplo de un administrador de clústeres externa. Un grupo de disponibilidad con el Administrador de clúster no tiene el tipo de clúster `NONE` los pasos de actualización que se describen aquí son específicos para los grupos de disponibilidad del tipo de clúster `EXTERNAL` o `NONE`.

1. Antes de comenzar, cada base de datos de copia de seguridad.
2. Actualizar las instancias de SQL Server que hospeden las réplicas secundarias.

    a. Actualice primero las réplicas secundarias asincrónicas.

    b. Actualizar las réplicas secundarias sincrónicas.

   >[!NOTE]
   >Si un grupo de disponibilidad solo tiene asincrónica réplicas - para evitar la pérdida de datos cambiar una réplica al sincrónica y esperan hasta que se sincronicen. A continuación, actualice esta réplica.

   b.1. Detener el recurso en el nodo que hospeda la réplica secundaria de destino para la actualización

   Antes de ejecutar el comando de actualización, detenga el recurso para que el clúster no se supervisará y producirá un error innecesariamente. En el ejemplo siguiente se agrega una restricción de ubicación en el nodo que se producirá en el recurso que se va a detener. Actualización `ag_cluster-master` con el nombre del recurso y `nodeName1` con el nodo que hospeda la réplica de destino para la actualización.

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>2. &nbsp;[Configurar SQL Server 2017 imágenes del contenedor en Docker](sql-server-linux-configure-docker.md)

*Actualizado: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. Identificar la Docker **etiqueta** para la versión que desea usar. Para ver las etiquetas disponibles, vea [la página del concentrador mssql-server-linux Docker](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Extraiga la imagen de contenedor de SQL Server con la etiqueta. Por ejemplo, para extraer la imagen de RC1, reemplace `<image_tag>` en el siguiente comando con `rc1`.

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. Para ejecutar un nuevo contenedor con esa imagen, especifique el nombre de etiqueta en el `docker run` comando. En el siguiente comando, reemplace `<image_tag>` con la versión que desea ejecutar.

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

Estos pasos también se pueden utilizar para degradar un contenedor existente. Por ejemplo, podría desea deshacer o degradar un contenedor en ejecución para la solución de problemas o las pruebas. Para degradar un contenedor en ejecución, debe utilizar una técnica de persistencia de la carpeta de datos. Siga los mismos pasos que se describen en la [actualizar sección--#upgrade), pero especifica el nombre de etiqueta de la versión más antigua cuando se ejecuta el nuevo contenedor.

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-configure-sql-server-on-linux-with-the-mssql-conf-toolsql-server-linux-configure-mssql-confmd"></a>3. &nbsp;[Configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md)

*Actualizado: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [siguiente](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a>Directorio del conjunto de auditoría local**


El **telemetry.userrequestedlocalauditdirectory** configuración habilita la auditoría Local y se crea permite establecer el directorio donde se registra la auditoría Local.

1. Cree un directorio de destino para los nuevos registros de auditoría Local. En el ejemplo siguiente se crea un nuevo **/tmp/auditoría** directorio:

```
   sudo mkdir /tmp/audit
```

1. Cambiar el propietario y el grupo del directorio para la **mssql** usuario:

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. Reinicie el servicio de SQL Server:

```
   sudo systemctl restart mssql-server
```

Para obtener más información, consulte [comentarios del cliente para SQL Server en Linux--sql-server-linux-customer-feedback.md).

**<a id="lcid"></a>Cambiar la configuración regional de SQL Server**


El **language.lcid** cambios en la configuración la configuración regional de SQL Server a cualquier identificador de idioma admitidos (LCID).

1. En el ejemplo siguiente se cambia la configuración regional en francés (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. Reinicie el servicio de SQL Server para aplicar los cambios:

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a>Establecer el límite de memoria**


El **memory.memorylimitmb** opción controla la cantidad memoria física (en MB) disponible para SQL Server. El valor predeterminado es 80% de la memoria física.

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **memory.memorylimitmb**. En el ejemplo siguiente se cambia la memoria disponible para SQL Server a 3,25 GB (3328 MB).

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. Reinicie el servicio de SQL Server para aplicar los cambios:



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-customer-feedback-for-sql-server-on-linuxsql-server-linux-customer-feedbackmd"></a>4. &nbsp;[Comentarios de los clientes de SQL Server en Linux](sql-server-linux-customer-feedback.md)

*Actualizado: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [siguiente](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**En Docker**

Para habilitar la auditoría Local en docker, debe tener Docker [conservar su data--sql-server-linux-configure-docker.md).

1. El directorio de destino para los nuevos registros de auditoría Local estará en el contenedor. Cree un directorio de destino para los nuevos registros de auditoría Local en el directorio de host en su equipo. En el ejemplo siguiente se crea un nuevo **/auditoría** directorio:

```
   sudo mkdir <host directory>/audit
```


1. Agregar un `mssql.conf` archivo con las líneas `[telemetry]` y `userrequestedlocalauditdirectory = <host directory>/audit` en el directorio de host:

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. Ejecutar la imagen de contenedor
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**Pasos siguientes**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restoresql-server-linux-migrate-restore-databasemd"></a>5. &nbsp;[Migrar una base de datos de SQL Server de Windows para Linux con backup y restore](sql-server-linux-migrate-restore-database.md)

*Actualizado: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [siguiente](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* Máquina de Windows con lo siguiente:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) instalado.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) instalado.
  * Base de datos de destino para migrar.

* Máquina Linux con instalado lo siguiente:
  * SQL Server de 2017 RC2. Vea los tutoriales de instalación para [RHEL--quickstart-install-connect-red-hat.md), [SLES--inicio rápido-install-conectarse-suse.md), o [Ubuntu--inicio rápido-install-conectarse-ubuntu.md).
  * SQL Server de 2017 RC2 [tools--sql-server-linux-setup-tools.md de línea de comandos).

**Cree una copia de seguridad en Windows**


Hay varias maneras de crear un archivo de copia de seguridad de una base de datos en Windows. Los pasos siguientes utilizan SQL Server Management Studio (SSMS).

1. Iniciar **SQL Server Management Studio** en su equipo de Windows.

1. En el cuadro de diálogo de conexión, escriba **localhost**.

1. En el Explorador de objetos, expanda **bases de datos**.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>6. &nbsp;[Notas de la versión de SQL Server 2017 en Linux](sql-server-linux-release-notes.md)

*Actualizado: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [siguiente](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a>RC2 (agosto de 2017)**


La versión del motor de SQL Server para esta versión es 14.0.900.75.

**Plataformas compatibles**


| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 | XFS o EXT4 | [Instalación guide--quickstart-install-connect-red-hat.md) |
| Service Pack 2 SUSE Enterprise Linux Server v12 | EXT4 | [Guía de instalación: inicio rápido-install-conectarse-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Guía de instalación: inicio rápido-install-conectarse-ubuntu.md) |
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación: inicio rápido-install-conectarse-docker.md) |

> [!NOTE]
> Necesita al menos 3,25 GB de memoria para ejecutar SQL Server en Linux.
> Motor de SQL Server ha sido probado hasta 1,5 TB de memoria en este momento.

**Detalles del paquete**


En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalación de paquete de SQL Server: sql-server-linux-setup.md)
- [Instalación package--sql-server-linux-setup-full-text-search.md de búsqueda de texto completo)
- [Instalación de agente SQL Server package--sql-server-linux-setup-sql-agent.md)

| Paquete | versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.900.75-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md)

*Actualizado: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [siguiente](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a>Revertir SQL Server**


Para revertir o degradación de SQL Server a una versión anterior, siga estos pasos:

1. Identifique el número de versión para el paquete de SQL Server que desea cambiar a. Para obtener una lista de números de paquete, consulte la [versión notes--sql-server-linux-release-notes.md).

1. Degradar a una versión anterior de SQL Server. En los siguientes comandos, reemplace `<version_number>` con el número de versión de SQL Server ha identificado en el paso uno.

   | Plataforma | Comandos de actualización de paquete |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES GRANDE | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Solo se admite para degradar a una versión dentro de la misma versión principal, como SQL Server 2017.

> [!IMPORTANT]
> Degradación solo se admite entre RC2 y RC1 en este momento.




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-install-sql-server-integration-services-ssis-on-linuxsql-server-linux-setup-ssismd"></a>8. &nbsp;[Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)

*Actualizado: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



Si ya tiene `mssql-server-is` instalado, puede actualizar a la versión más reciente con el siguiente comando:

```
sudo apt-get install mssql-server-is
```


Para quitar `mssql-server-is`, puede ejecutar el comando siguiente:
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a>Instalar SSIS en RHEL**

Para instalar el `mssql-server-is` el paquete en RHEL, siga estos pasos:


1.  ENTRAR en el modo de superusuario.

```
    sudo su
```


2.  Descargue el archivo de configuración del repositorio de Microsoft SQL Server Red Hat.

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  Salir del modo de superusuario.

```
    exit
```


4.  Ejecute los comandos siguientes para instalar SQL Server Integration Services.

```
    sudo yum install -y mssql-server-is
```


5.  Después de la instalación, vuelva a ejecutar `ssis-conf`.







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

En esta sección se enumera los artículos muy similar para los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (3 + 12): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (5 + 0): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (5 + 1): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (19 + 82): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (1 + 8): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (12 + 1): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (0 + 1): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (7 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (1 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (0 + 2): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (1 + 4): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (4 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Nuevos y actualizados (0 + 1): **Tools para SQL** documentos](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos y actualizados (0 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos y actualizados (0 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)



