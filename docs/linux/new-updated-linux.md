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
ms.date: 07/17/2017
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 13c237af359c543f6a99a0fce101af81b5eb2bcf
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Las nuevas y recientemente actualizado: SQL Server en documentos de Linux

Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-05-23** &nbsp; - a - &nbsp; **2017-07-17**
- *Área de asunto:* &nbsp; **Microsoft SQL Server en Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Ejecutar la imagen de contenedor de SQL Server 2017 con Docker](quickstart-install-connect-docker.md)
2. [Instalar a SQL Server y crear una base de datos en Red Hat](quickstart-install-connect-red-hat.md)
3. [Instalar a SQL Server y crear una base de datos en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
4. [Instalar a SQL Server y crear una base de datos en Ubuntu](quickstart-install-connect-ubuntu.md)
5. [Ejemplo: Script de instalación desatendida de SQL Server para Red Hat Enterprise Linux](sample-unattended-install-redhat.md)
6. [Ejemplo: Script de instalación desatendida de SQL Server para SUSE Linux Enterprise Server](sample-unattended-install-suse.md)
7. [Ejemplo: Script de instalación desatendida de SQL Server para Ubuntu](sample-unattended-install-ubuntu.md)
8. [Autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md)
9. [Alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md)
10. [Configurar SQL Server 2017 imágenes del contenedor en Docker](sql-server-linux-configure-docker.md)
11. [Comentarios de los clientes de SQL Server en Linux](sql-server-linux-customer-feedback.md)
12. [Cifrado de las conexiones a SQL Server en Linux](sql-server-linux-encrypted-connections.md)
13. [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección de citas.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que han presentado recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-sles-cluster-for-sql-server-availability-groupsql-server-linux-availability-group-cluster-slesmd"></a>1. &nbsp;[Configuración de clúster SLES para grupo de disponibilidad de SQL Server](sql-server-linux-availability-group-cluster-sles.md)

*Updated: 2017-06-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 189.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f8d28af253be1dc67615f1ea04135b2f6dff3b71 8be07deddcf0c348d75bf5b4f44615c2383e0722  (PR=2150  ,  Filename=sql-server-linux-availability-group-cluster-sles.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=6dccaff93a6c8b2374a1fad069b2f597898802fc) -->



**Establecer propiedades de clúster inicio error-es-grave en false**


`Start-failure-is-fatal`indica si un error al iniciar un recurso en un nodo impide más intentos de inicio en ese nodo. Cuando se establece en `false`, el clúster decidirá si se intente iniciar en el mismo nodo nuevo, en función actual error recuento y migración el umbral del recurso. Por lo tanto, después de producirse la conmutación por error, marcapasos volverá a intentar iniciar el recurso de grupo de disponibilidad en la primera estructura principal una vez que la instancia de SQL está disponible. Marcapasos se encargará de degradación de la réplica secundaria y vuelve a unir automáticamente el grupo de disponibilidad. Además, si `start-failure-is-fatal` se establece en `false`, el clúster recurra a los límites configurados failcount configurados con el umbral de migración, por lo que debe realizar de forma predeterminada seguro para el umbral de migración se actualiza en consecuencia.

Para actualizar el valor de propiedad para ejecución false:
```
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
Si la propiedad tiene el valor predeterminado de `true`, si el primer intento de iniciar el recurso se produce un error, la intervención del usuario es necesario después de una conmutación por error automática para realizar la limpieza el recuento de errores de recursos y restablece la configuración mediante: `sudo crm resource cleanup <resourceName>` comando.

Para obtener más información sobre propiedades de clúster marcapasos, consulte [configurar recursos de clúster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

**Configurar la barrera (STONITH)**

Los proveedores de clúster marcapasos requieren STONITH esté habilitado y un dispositivo de barrera configurado para una instalación de clúster compatibles. Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, barrera se utiliza para poner el clúster en un estado conocido de nuevo.
Barrera de nivel de recurso principalmente garantiza que no hay ningún daños en los datos en el caso de una interrupción del sistema mediante la configuración de un recurso. Puede usar la barrera de nivel de recurso, por ejemplo, con DRBD (Distributed replican bloque dispositivo) para marcar el disco en un nodo como obsoleto cuando el vínculo de comunicación deja de funcionar.




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-release-notes-for-sql-server-2017-on-linuxsql-server-linux-release-notesmd"></a>2. &nbsp;[Notas de la versión de SQL Server 2017 en Linux](sql-server-linux-release-notes.md)

*Updated: 2017-06-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 156.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 684da20f7834000886d7a93f83563c55dc3cf9a6 8597bcde7e5754bb7f38de1ec980027245dac6e5  (PR=2115  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=424a23fd98876db808b91f017e7acbcb5b4daa45) -->



**SQL Server Integration Services (SSIS)**

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





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>Artículos similares

En esta sección se enumera los artículos muy similar para los artículos actualizados recientemente en otras áreas temáticas, dentro del mismo repositorio GitHub.com: [MicrosoftDocs /**pr de documentos de sql**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas que disponga de artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (4 + 4): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (2 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (1 + 2): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (6 + 0): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (13 + 2): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (1 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (1 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (4 de 8 +): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (2 + 2): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (0 + 1): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (1 + 0): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Nuevos y actualizados (1 + 0): **Tools para SQL** documentos](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas que no disponga de ninguna artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (0 + 0): **ActiveX Data Objects (ADO) para SQL** documentos](../ado/new-updated-ado.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos y actualizados (0 + 0): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Nuevos y actualizados (0 + 0): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (0 + 0): **ejemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)


&nbsp;


