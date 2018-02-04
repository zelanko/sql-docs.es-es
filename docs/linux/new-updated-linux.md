---
title: 'Actualizado: SQL Server en documentos de Linux | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Microsoft SQL Server en Linux."
services: na
documentationcenter: 
author: MightyPen
manager: craigg
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: d477af0c4c7027892d4ade8e586c9a9b908a05ea
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Las nuevas y recientemente actualizado: SQL Server en documentos de Linux



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de asunto:* &nbsp; **Microsoft SQL Server en Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Ejecutar el servidor de SQL 2017 en la nube](quickstart-install-connect-clouds.md)
2. [Repositorios de cambio desde el repositorio de vista previa en el repositorio de GA](sql-server-linux-change-repo.md)
3. [Prácticas recomendadas de rendimiento y directrices de configuración para SQL Server 2017 en Linux](sql-server-linux-performance-best-practices.md)
4. [Instancias de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-concepts.md)
5. [Configurar la instancia de clúster de conmutación por error - iSCSI: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
6. [Configurar la instancia de clúster de conmutación por error - NFS: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
7. [Configurar la instancia de clúster de conmutación por error - SMB - SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)
8. [Funcionan de la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-operate.md)
9. [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
10. [Restaurar una base de datos de SQL Server en un contenedor Linux Docker](tutorial-restore-backup-in-sql-server-container.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Ejecutar la imagen de contenedor de SQL Server 2017 con Docker](#TitleNum_1)
2. [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](#TitleNum_2)
3. [Alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](#TitleNum_3)
4. [Configurar SQL Server 2017 imágenes del contenedor en Docker](#TitleNum_4)
5. [Cifrado de las conexiones a SQL Server en Linux](#TitleNum_5)
6. [Crear y ejecutar trabajos del Agente SQL Server en Linux](#TitleNum_6)
7. [Guía de instalación para SQL Server en Linux](#TitleNum_7)
8. [Configurar la instancia de clúster de conmutación por error: SQL Server en Linux (RHEL)](#TitleNum_8)
9. [Solucionar problemas de SQL Server en Linux](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-run-the-sql-server-2017-container-image-with-dockerquickstart-install-connect-dockermd"></a>1. &nbsp;[Ejecutar la imagen de contenedor de SQL Server 2017 con Docker](quickstart-install-connect-docker.md)

*Actualizado: 30-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 261.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2aaf953c2f1fb675b1304186108fbef1eebf6f8f f7cd42bb320a8892a5ec63ce999186438097636a  (PR=4150  ,  Filename=quickstart-install-connect-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**Quitar el contenedor**


Si desea quitar el contenedor de SQL Server que se usan en este tutorial, ejecute los siguientes comandos:

```
sudo docker stop sql1
sudo docker rm sql1
```

```
docker stop sql1
docker rm sql1
```

> [!WARNING]
> Detener y quitar un contenedor de forma permanente eliminan los datos de SQL Server en el contenedor. Si tiene que conservar los datos, [crear y copiar un archivo de copia de seguridad fuera de la container--tutorial-restore-backup-in-sql-server-container.md) o usar una [contenedor persistencia de los datos technique--sql-server-linux-configure-docker.md#persist).




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-configure-always-on-availability-group-for-sql-server-on-linuxsql-server-linux-availability-group-configure-hamd"></a>2. &nbsp;[Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 129.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c7e6bc862e5b062a855918efbeee5fe748b7236 6900c9a30ce04ce54e7aaa270ef7d276c18f9afd  (PR=4150  ,  Filename=sql-server-linux-availability-group-configure-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



- Crear grupo de disponibilidad con dos réplicas sincrónicas y una réplica de configuración:

   >[!IMPORTANT]
   >Esta arquitectura permite que cualquier edición de SQL Server para hospedar la réplica terceros. Por ejemplo, la tercera réplica se puede hospedar en SQL Server Enterprise Edition. En Enterprise Edition, es el tipo de extremo solo es válido `WITNESS`.

```sql
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
       N'**<node1>**' WITH (
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node2>**' WITH (
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
          FAILOVER_MODE = EXTERNAL,
          SEEDING_MODE = AUTOMATIC
          ),
       N'**<node3>**' WITH (
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**',
          AVAILABILITY_MODE = CONFIGURATION_ONLY
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-high-availability-and-data-protection-for-availability-group-configurationssql-server-linux-availability-group-hamd"></a>3. &nbsp;[Alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [siguiente](#TitleNum_4))

<!-- Source markdown line 106.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e6bee794ce19f1ed62298b4a0cce7207550f1595 b64726cd6e91721850721786d26c170d59fc320a  (PR=4150  ,  Filename=sql-server-linux-availability-group-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



El valor predeterminado de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` es 0. En la tabla siguiente se describe el comportamiento de disponibilidad.

| |Alta disponibilidad & </br> protección de datos | Protección de los datos
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Interrupción principal | Conmutación por error automática. Nuevo elemento principal es R / w. | Conmutación por error automática. Nuevo elemento principal no está disponible para las transacciones de usuario.
|Interrupción de la réplica secundaria | Principal es de lectura/escritura, ejecución expuesta a la pérdida de datos (si principal produce un error y no se puede recuperar). No hay conmutación automática por error si falla el sitio primario también. | Principal no está disponible para las transacciones de usuario. No hay ninguna réplica para conmutar a si falla el sitio primario también.
|Interrupción de réplica solo configuración | Principal es R / w. No hay conmutación automática por error si falla el sitio primario también. | Principal es R / w. No hay conmutación automática por error si falla el sitio primario también.
|Elemento secundario sincrónico + configuración solo interrupción de réplica| Principal no está disponible para las transacciones de usuario. No hay conmutación por error automática. | Principal no está disponible para las transacciones de usuario. No hay ninguna réplica en conmutación por error como si también generará errores principales.
<sup>*</sup>Valor predeterminado

>[!NOTE]
>La instancia de SQL Server que hospeda la única réplica de configuración también puede hospedar otras bases de datos. También puede participar como una configuración única base de datos de más de un grupo de disponibilidad.

**Requisitos**


* Todas las réplicas de un grupo de disponibilidad con una única réplica de configuración deben ser SQL Server 2017 CU 1 o posterior.
* Cualquier edición de SQL Server puede hospedar una réplica de solo de configuración, incluido SQL Server Express.
* El grupo de disponibilidad necesita al menos una réplica secundaria - además de la réplica principal.
* Réplicas sola de configuración no se cuentan en el número máximo de réplicas por instancia de SQL Server. SQL Server standard edition permite hasta tres réplicas, SQL Server Enterprise Edition permite hasta 9.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-configure-sql-server-2017-container-images-on-dockersql-server-linux-configure-dockermd"></a>4. &nbsp;[Configurar SQL Server 2017 imágenes del contenedor en Docker](sql-server-linux-configure-docker.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [siguiente](#TitleNum_5))

<!-- Source markdown line 34.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c759fb88ae8d654414202f28c5fc58dfd02581bf fd270118f2f4608fceaf563fc143951b41097bdb  (PR=4150  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



En este tema de configuración proporciona los escenarios de uso adicionales en las secciones siguientes.

**<a id="production"></a>Ejecute las imágenes del contenedor de producción**


El inicio rápido en la sección anterior, ejecuta la edición de desarrollador gratuita de SQL Server de Docker Hub. La mayor parte de la información sigue siendo válido si va a ejecutar imágenes de contenedor, como las ediciones Enterprise, Standard o Web de producción. Sin embargo, hay algunas diferencias que se describen a continuación.

- Sólo se puede utilizar SQL Server en un entorno de producción si tiene una licencia válida. Puede obtener una licencia de producción de SQL Server Express gratuita [aquí](https://go.microsoft.com/fwlink/?linkid=857693). Licencias de SQL Server Standard y Enterprise Edition están disponibles a través de [Microsoft Volume Licensing](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs.aspx).

- Imágenes de contenedor de SQL Server de producción deben extraerse de [Docker almacén](https://store.docker.com). Si aún no tiene uno, cree una cuenta en el almacén de Docker.

- La imagen del contenedor para desarrolladores en el almacén de Docker puede configurarse para ejecutarse también las ediciones de producción. Utilice los pasos siguientes para ejecutar las ediciones de producción:

   1. En primer lugar, inicie sesión en el identificador de docker desde la línea de comandos.

```
      docker login
```

   1. A continuación, debe obtener el desarrollador gratuita imagen de contenedor en el almacén de Docker. Vaya a [https://store.docker.com/images/mssql-server-linux](https://store.docker.com/images/mssql-server-linux), haga clic en **desproteger**y siga las instrucciones.

   1. Revise los requisitos y ejecutar procedimientos en el [inicio rápido: inicio rápido-install-conectarse-docker.md). Pero hay dos diferencias. Se debe extraer de la imagen **almacén/microsoft/mssql-server-linux:\<nombre de etiqueta\>**  del almacén de Docker. Debe especificar la edición de producción con el **MSSQL_PID** variable de entorno. En el ejemplo siguiente se muestra cómo ejecutar la imagen de contenedor de SQL Server 2017 más reciente para la edición Enterprise:



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-encrypting-connections-to-sql-server-on-linuxsql-server-linux-encrypted-connectionsmd"></a>5. &nbsp;[Cifrado de las conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [siguiente](#TitleNum_6))

<!-- Source markdown line 45.  ms.author= meetb;rickbyh.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e3187866df060903e30000d60d673edad46d210 bcb1f2771e6c29b535a30b9f23ac296954509187  (PR=4150  ,  Filename=sql-server-linux-encrypted-connections.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



        sudo chown mssql:mssql mssql.pem mssql.key
        sudo chmod 600 mssql.pem mssql.key
        sudo mv mssql.pem /etc/ssl/certs/
        sudo mv mssql.key /etc/ssl/private/

- **Configurar SQL Server**

        systemctl stop mssql-server
        cat /var/opt/mssql/mssql.conf
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssqlfqdn.pem
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssqlfqdn.key
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0

- **Registrar el certificado en el equipo cliente (Windows, Linux o Mac OS)**

    -   Si usas certificado firmado de CA tendrá que copiar el certificado de entidad de certificación (CA) en lugar del certificado de usuario en el equipo cliente.
    -   Si está utilizando el certificado autofirmado simplemente copie el archivo PEM en las siguientes carpetas correspondientes a la distribución y ejecute los comandos para habilitarlos

        - **Windows**: importar el archivo PEM como un certificado de usuario actual -> entidades de certificación raíz -> certificados de confianza
        - **macOS**:

-   **Ejemplos de cadena de conexión**

    - **..!NCLUDE-NotShown--ssmanstudiofull-md--../includes/ssmanstudiofull-md.md)]** ![SSMS connection dialog--media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "SSMS connection dialog")



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-create-and-run-sql-server-agent-jobs-on-linuxsql-server-linux-run-sql-server-agent-jobmd"></a>6. &nbsp;[Creación y ejecución de trabajos de agente SQL Server en Linux](sql-server-linux-run-sql-server-agent-job.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [siguiente](#TitleNum_7))

<!-- Source markdown line 35.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1598129bb5f98434435d8ad02336a9adf76c7870 6fe3fe7df3a60dbac31f1df59aac9860d293421a  (PR=4150  ,  Filename=sql-server-linux-run-sql-server-agent-job.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Los siguientes requisitos previos son necesarios para completar este tutorial:

* Máquina Linux con los siguientes requisitos previos:
  * SQL Server 2017 ([RHEL--quickstart-install-connect-red-hat.md), [SLES--inicio rápido-install-conectarse-suse.md), o [Ubuntu--inicio rápido-install-conectarse-ubuntu.md)) con las herramientas de línea de comandos.

Los requisitos previos siguientes son opcionales:

* Máquina de Windows con SSMS:
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para pasos opcionales de SSMS.

**Instalar el Agente SQL Server**


Para utilizar el Agente SQL Server en Linux, primero debe instalar la **agente de server mssql** paquete en un equipo que ya tenga SQL Server 2017 instalado.

1. Instalar **mssql-server-agent** con el comando apropiado para su sistema operativo Linux.

   | Plataforma | Comandos de instalación |
   |-----|-----|
   | RHEL | `sudo yum install mssql-server-agent` |
   | SLES GRANDE | `sudo zypper refresh`<br/>`sudo zypper update mssql-server-agent` |
   | Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server-agent` |

1. Reinicie SQL Server con el siguiente comando:

```
   sudo systemctl restart mssql-server
```

**Crear una base de datos de ejemplo**


Siga estos pasos para crear una base de datos de ejemplo denominada **SampleDB**. Esta base de datos se usa para el trabajo de copia de seguridad diario.

1. En el equipo Linux, abra una sesión de terminal de bash.



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-installation-guidance-for-sql-server-on-linuxsql-server-linux-setupmd"></a>7. &nbsp;[Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md)

*Actualizado: 2017-12-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [siguiente](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880 eedddcfb64c6432215f56b74dc91700d9804fce8  (PR=4160  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=085dd05d56afecbb454206ed8402cfbaa597cfbe) -->



**<a id="repositories"></a>Configurar repositorios de origen**


Al instalar o actualizar SQL Server, obtendrá la versión más reciente de SQL Server desde el repositorio de Microsoft configurado.

**Opciones de repositorio**


Hay dos tipos principales de repositorios para cada distribución:

- **Las actualizaciones acumulativas (CU)**: repositorio de actualización acumulativa The (CU) contiene los paquetes para la versión de SQL Server base y cualquier correcciones o mejoras desde esa versión. Las actualizaciones acumulativas son específicas de una versión de lanzamiento, por ejemplo, SQL Server 2017. Se publican a un ritmo regular.

- **GDR**: repositorio el GDR contiene paquetes para la versión de SQL Server base y solo correcciones críticas y actualizaciones de seguridad desde esa versión. Estas actualizaciones también se agregan a la próxima versión CU.

Cada versión CU y GDR contiene el paquete completo de SQL Server y todas las actualizaciones anteriores para ese repositorio. Se admite la actualización desde una versión GDR a una versión CU cambiando su repositorio configurado para SQL Server. También puede [degradar--#rollback) a cualquier versión dentro de la versión principal (por ejemplo: 2017). Actualizar desde una CU no se admite la versión a una versión GDR.

**Compruebe su repositorio configurado**


Si desea comprobar qué repositorio está configurada, utilice las siguientes técnicas depende de la plataforma.

| Plataforma | Procedimiento |
|-----|-----|
| RHEL | 1. Ver los archivos en el **/etc/yum.repos.d** directorio:`sudo ls /etc/yum.repos.d`<br/>2. Busque un archivo que configura el directorio de SQL Server, como **server.repo mssql**.<br/>3. Imprimir el contenido del archivo:`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4. El **nombre** propiedad es el repositorio configurado.|
| SLES GRANDE | 1. Ejecute el siguiente comando: `sudo zypper info mssql-server`<br/>2. El **repositorio** propiedad es el repositorio configurado. |
| Ubuntu | 1. Ejecute el siguiente comando: `sudo cat /etc/apt/sources.list`<br/>2. Examine la dirección URL del paquete para servidor mssql. |



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-configure-failover-cluster-instance---sql-server-on-linux-rhelsql-server-linux-shared-disk-cluster-configuremd"></a>8. &nbsp;[Instancia de clúster de conmutación por error de configuración: SQL Server en Linux (RHEL)](sql-server-linux-shared-disk-cluster-configure.md)

*Actualizado: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7) | [siguiente](#TitleNum_9))

<!-- Source markdown line 25.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 308fa1809c80a009f7f15b5ca6917f6b76588c3e 71f18baa320041ff10c94e8c7668e40dff45cac3  (PR=4150  ,  Filename=sql-server-linux-shared-disk-cluster-configure.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



> [!div class="checklist"]
> * Instalar y configurar Linux
> * Instalar y configurar SQL Server
> * Configurar el archivo de hosts
> * Configurar el almacenamiento compartido y mueva los archivos de base de datos
> * Instalar y configurar a marcapasos en cada nodo del clúster
> * Configurar la instancia de clúster de conmutación por error

En este artículo se explica cómo crear una instancia de clúster de conmutación por error (FCI) de disco compartido de dos nodos para SQL Server. El artículo incluye instrucciones y ejemplos de secuencias de comandos para Red Hat Enterprise Linux (RHEL). Ubuntu distribuciones son similares a RHEL de manera que los ejemplos de secuencias de comandos normalmente lo hará también funcionan en Ubuntu.

Para obtener información conceptual, consulte [SQL Server conmutación por error de instancia de clúster (FCI) en Linux--sql-server-linux-shared-disk-cluster-concepts.md).

**Requisitos previos**


Para completar el siguiente escenario de extremo a extremo debe tener dos máquinas para implementar el clúster de dos nodos y otro servidor para el almacenamiento. Pasos siguientes describen cómo se configurarán estos servidores.

**Instalar y configurar Linux**


El primer paso es configurar el sistema operativo en los nodos del clúster. En cada nodo del clúster, configure una distribución de linux. Utilice la misma distribución y la versión en ambos nodos. Utilice uno de los dos de las siguientes distribuciones:

* RHEL con una suscripción válida para el complemento de alta disponibilidad

**Instalar y configurar SQL Server**


1. Instalar y configurar SQL Server en ambos nodos.  Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux: sql-server-linux-setup.md).
1. Designar un nodo como principal y el otro como secundario para fines de configuración. Utilizando estos términos para los siguientes elementos en esta guía.
1. En el nodo secundario, detenga y deshabilite a SQL Server.
    En el ejemplo siguiente se detiene y deshabilita a SQL Server:
```
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
```

    > [!NOTE]
    > At set up time, a Server Master Key is generated for the SQL Server instance and placed at `var/opt/mssql/secrets/machine-key`. On Linux, SQL Server always runs as a local account called mssql. Because it's a local account, its identity isn't shared across nodes. Therefore, you need to copy the encryption key from primary node to each secondary node so each local mssql account can access it to decrypt the Server Master Key.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-troubleshoot-sql-server-on-linuxsql-server-linux-troubleshooting-guidemd"></a>9. &nbsp;[Solucionar problemas de SQL Server en Linux](sql-server-linux-troubleshooting-guide.md)

*Actualización: 30-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_8))

<!-- Source markdown line 125.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f8557a34b38e028ff6e5ac370b6d2d6bf315091 196e56187b57bdd79cc5cdc5e6fce3d41e82af0c  (PR=4150  ,  Filename=sql-server-linux-troubleshooting-guide.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



**Inicie SQL Server con la configuración mínima o en modo de usuario único**


**Iniciar SQL Server en modo de configuración mínima**

Esta opción resulta útil si el valor de una opción de configuración (por ejemplo, la confirmación excesiva de memoria) ha impedido el inicio del servidor.

```
   sudo -u mssql /opt/mssql/bin/sqlservr -f
```

**Iniciar SQL Server en modo de usuario único**

En determinadas circunstancias, tendrá que iniciar una instancia de SQL Server en modo de usuario único mediante la opción de inicio -m. Por ejemplo, es posible que desee cambiar las opciones de configuración del servidor o recuperar una base de datos maestra dañada u otra base de datos del sistema. Por ejemplo, puede que desee cambiar las opciones de configuración de servidor o recuperar una base de datos maestra dañada u otra base de datos del sistema

Iniciar SQL Server en modo de usuario único
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m
```

Iniciar SQL Server en modo de usuario único con SQLCMD
```
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
```

> [!WARNING]
>  Inicie SQL Server en Linux con el usuario "mssql" para evitar problemas de inicio futuros. Ejemplo "sudo -u mssql /opt/mssql/bin/sqlservr [OPCIONES DE INICIO]"

Si accidentalmente han iniciado SQL Server con otro usuario, debe cambiar la propiedad de los archivos de base de datos de SQL Server al usuario antes de iniciar SQL Server con systemd 'mssql'. Por ejemplo, para cambiar la propiedad de todos los archivos de base de datos en /var/opt/mssql para el usuario 'mssql', ejecute el siguiente comando

```
   chown -R mssql:mssql /var/opt/mssql/
```







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas que disponga de artículos nuevos o actualizados recientemente

- [Nuevos + Actualizados (3+14): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (1 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (87+0): documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + Actualizados (5+4): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + Actualizados (0+1): documentos de **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + Actualizados (2+2): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + Actualizados (10+9): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + Actualizados (2+4): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + Actualizados (4+2): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + Actualizados (0+1): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (21+0): documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + Actualizados (5+1): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (0 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos + Actualizados (1+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (0 + 1): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos + Actualizados (0+2): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas que no disponga de ninguna artículos nuevos o actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos y actualizados (0 + 0): **ActiveX Data Objects (ADO) para SQL** documentos](../ado/new-updated-ado.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)


