---
title: Documentos actualizados sobre el motor de base de datos | Microsoft Docs
description: Muestra fragmentos de contenido actualizado de la documentación modificada recientemente relativa al motor de base de datos.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: database-engine
ms.date: 02/03/2018
ms.openlocfilehash: cc728acbbf5bdc9fb4c8547d4d85b1d578f4e1dc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-database-engine-docs"></a>Documentos nuevos y actualizados recientemente sobre el motor de base de datos



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-12-2017** &nbsp; al &nbsp; **03-02-2018**
- *Área de asunto:* &nbsp; **motor de base de datos**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


***En este momento no hay ningún artículo nuevo en la lista.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Actualización de instancias de la réplica del grupo de disponibilidad Always On](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-upgrading-always-on-availability-group-replica-instancesavailability-groupswindowsupgrading-always-on-availability-group-replica-instancesmd"></a>1. &nbsp; [Actualización de instancias de la réplica del grupo de disponibilidad Always On](availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)

*Actualizado: 29-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 174.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 20ca282e8965889a7a530fb67e125cc876410e41 9f27d0f9a74333b291c1cdc1529edc13960fae29  (PR=4741  ,  Filename=upgrading-always-on-availability-group-replica-instances.md  ,  Dirpath=docs\database-engine\availability-groups\windows\  ,  MergeCommitSha40=0a44ce9993ebf61f86e409255a1d58d47993951a) -->



**Pasos especiales para la replicación o captura de datos modificados**


Dependiendo de la actualización que se aplique, es posible que sea necesario realizar pasos adicionales para bases de datos de réplica de AG habilitados para replicar o capturar datos modificados. Consulte las notas de la versión de la actualización para determinar si necesita realizar los siguientes pasos o no:

1. Actualice todas las réplicas secundarias.

1. Tras actualizar todas las réplicas secundarias, conmute por error el AG en una instancia actualizada.

1. Ejecute el siguiente comando de Transact-SQL en la instancia que hospeda la réplica principal:

   ```
   EXECUTE [master].[sys].[sp_vupgrade_replication];
   ```

   >[!NOTE]
   >La ejecución de este comando puede llevar varios minutos.

1. Actualice la instancia que estaba originalmente en la réplica principal.

Para obtener información general, consulte [CDC functionality may break after upgrading to the latest CU](http://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/) (Es posible que la funcionalidad CDC no funcione después de actualizar a la última CU).









## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente


- [Nuevos + actualizados (1+3): &nbsp;documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos del **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (12+1): **documentos de** Integration Services para SQL](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (6+2): &nbsp;documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (15+0): **documentos de** PowerShell para SQL](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (2+9): &nbsp;documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (1+0): &nbsp;documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (1+1): &nbsp;documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + actualizados (1+1): &nbsp;documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (1+2): &nbsp;documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (0+2): &nbsp;documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente


- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../samples/new-updated-samples.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


