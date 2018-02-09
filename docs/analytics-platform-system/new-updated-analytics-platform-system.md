---
title: 'Actualizado: Analytics Platform System para documentos de SQL Server | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Analytics Platform System para Microsoft SQL Server."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: aps-pdw
ms.date: 02/03/2018
ms.openlocfilehash: 2ae6339897b52cd16ad3417cc218afe1df95ba2a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-analytics-platform-system-for-sql-server"></a>Nuevos y actualizados recientemente: Analytics Platform System para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-12-03** &nbsp; - a - &nbsp; **2018-02-03**
- *Área de asunto:* &nbsp; **Analytics Platform System para SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


***En este momento no hay ningún artículo nuevo en la lista.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Configurar la conectividad de PolyBase para datos externos](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-configure-polybase-connectivity-to-external-dataconfigure-polybase-connectivity-to-external-datamd"></a>1. &nbsp;[Configurar la conectividad de PolyBase para datos externos](configure-polybase-connectivity-to-external-data.md)

*Actualizado: 2018-01-29* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 132.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 947f789480da66b9f636f39b30caec6be60d8c4d d4d4d45fbbb8e10ed6f26fe12f9a25d2e8e4f068  (PR=4741  ,  Filename=configure-polybase-connectivity-to-external-data.md  ,  Dirpath=docs\analytics-platform-system\  ,  MergeCommitSha40=0a44ce9993ebf61f86e409255a1d58d47993951a) -->



**Configuración de Kerberos**

Tenga en cuenta que cuando PolyBase se autentica en un clúster seguro de Kerberos, la configuración de hadoop.rpc.protection debe establecerse para la autenticación. Esto hace que la comunicación de datos entre nodos de Hadoop sin cifrar.

 Para conectarse a un clúster de Hadoop protegido con Kerberos [mediante MIT KDC]:


1.  Busque el directorio de configuración de Hadoop en la ruta de instalación en el nodo de Control:

    ```
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```

2.  Busque el valor de configuración del lado de Hadoop de las claves de configuración que se muestran en la tabla. (En el equipo de Hadoop, busque los archivos en el directorio de configuración de Hadoop).

3.  Copie los valores de configuración en la propiedad value en los archivos correspondientes en el nodo de Control.

    |**#**|**Archivo de configuración**|**Clave de configuración**|**Acción**|
    |------------|----------------|---------------------|----------|
    |1|core-site.xml|polybase.kerberos.kdchost|Especifique el nombre de host KDC. Por ejemplo: kerberos.su-dominio.com.|
    |2|core-site.xml|polybase.kerberos.realm|Especifique el dominio Kerberos. Por ejemplo: SU-DOMINIO.COM|
    |3|core-site.xml|hadoop.security.authentication|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: KERBEROS<br></br>**Nota de seguridad:** KERBEROS debe estar en mayúsculas. Si aparece en minúsculas, puede que no esté activado.|
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, hdfs/_HOST@YOUR-REALM.COM|
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo, mapred/_HOST@YOUR-REALM.COM|
    |6|mapred-site.xml|mapreduce.jobhistory.address|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: 10.193.26.174:10020|
    |7|yarn-site.xml yarn.|yarn.resourcemanager.principal|Busque la configuración del lado de Hadoop y cópiela en el equipo de SQL Server. Por ejemplo: yarn/_HOST@YOUR-REALM.COM|







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de asunto que *hacer* se nuevas o recientemente actualizado artículos


- [Nuevos y actualizados (1 + 3):&nbsp; **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (12 + 1): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (6 + 2):&nbsp; **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (15 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Nuevos y actualizados (2 + 9):&nbsp; **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (1 + 0):&nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (1 + 1):&nbsp; **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (1 + 1):&nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2):&nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Asunto áreas que realizan *no* cualquier nuevo o recientemente actualizaron artículos


- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos y actualizados (0 + 0): **ActiveX Data Objects (ADO) para SQL** documentos](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (0 + 0): **ejemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)


