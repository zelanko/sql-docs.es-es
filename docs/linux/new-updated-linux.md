---
title: 'Actualizado: SQL Server en documentos de Linux | Documentos de Microsoft'
description: Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Microsoft SQL Server en Linux.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: sql-linux,UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: ''
ms.date: 02/03/2018
ms.openlocfilehash: c277f51ddb50dfb9a5ef2bd23af7f6e80d00c25c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Las nuevas y recientemente actualizado: SQL Server en documentos de Linux



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-12-2017** &nbsp; al &nbsp; **03-02-2018**
- *Área de asunto:* &nbsp; **Microsoft SQL Server en Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Configurar instancias de clúster de conmutación por error y varias subredes grupos de disponibilidad AlwaysOn](sql-server-linux-configure-multiple-subnet.md)
2. [Crear y configurar un grupo de disponibilidad para SQL Server en Linux](sql-server-linux-create-availability-group.md)
3. [Implementar un clúster marcapasos para SQL Server en Linux](sql-server-linux-deploy-pacemaker-cluster.md)
4. [SQL Server en Linux preguntas más frecuentes (P+F)](sql-server-linux-faq.md)
5. [Conceptos básicos de la disponibilidad de SQL Server para las implementaciones de Linux](sql-server-linux-ha-basics.md)
6. [Configurar un contenedor de SQL Server en Kubernetes para alta disponibilidad](tutorial-sql-server-containers-kubernetes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Grupos de disponibilidad AlwaysOn en Linux](#TitleNum_1)
2. [Extraer, transformar y cargar datos en Linux con SSIS](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-always-on-availability-groups-on-linuxsql-server-linux-availability-group-overviewmd"></a>1. &nbsp;[Grupos de disponibilidad AlwaysOn en Linux](sql-server-linux-availability-group-overview.md)

*Actualizado: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 85.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 85685bc8ad3528aa26ca3f2bba7b0112808ad6f9 51aff6e55104c8f775d2b4f4461e44f689a9ee6b  (PR=4768  ,  Filename=sql-server-linux-availability-group-overview.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



Conmutación automática por error de un grupo de disponibilidad es posible cuando se cumplen las condiciones siguientes:

-   El servidor principal y la réplica secundaria se establecen en el movimiento de datos sincrónica.
-   La base de datos secundaria tiene un estado sincronizado (no sincronizar), lo que significa que los dos están en el mismo punto de datos.
-   El tipo de clúster está establecido como externo. Conmutación automática por error no es posible con un tipo de clúster de None.
-   El `sequence_number` de la réplica secundaria se convierta en el servidor principal tiene el número de secuencia superior: en otras palabras, la réplica secundaria `sequence_number` coincide con la de la réplica principal original.

Si se cumplen estas condiciones y se produce un error en el servidor que hospeda la réplica principal, el AG cambiará la propiedad a una réplica sincrónica. El comportamiento de réplicas sincrónicas (de lo que puede haber tres total: uno principal y dos réplicas secundarias) puede controlarse aún más mediante `required_synchronized_secondaries_to_commit`. Esto funciona con grupos de disponibilidad en Windows y Linux, pero se configura de forma totalmente diferente. En Linux, el valor se configura automáticamente el clúster en el propio recurso de AG.

**Quórum y la réplica solo configuración**


También es nueva en SQL Server 2017 a partir de CU1 una réplica de solo configuración. Porque marcapasos es diferente de un WSFC, especialmente cuando se trata de quórum y la necesidad de STONITH, con una configuración de dos nodos no funcionará cuando se trata de un AG. Una FCI, los mecanismos de quórum proporcionados por marcapasos pueden ser un problema, porque todos los arbitraje de conmutación por error FCI ocurre en el nivel de clúster. Para un AG, arbitraje en Linux se realiza en SQL Server, donde se almacenan todos los metadatos. Se trata en la réplica de solo configuración entra en juego.

Sin nada más, un tercer nodo y al menos una réplica sincronizada sería necesarios. Esto no funciona para SQL Server Standard, ya que puede contener solo dos réplicas que participan en un AG. La réplica de solo configuración almacena la configuración de AG en la base de datos maestra, igual que las otras réplicas en la configuración de AG. La réplica de solo configuración no tiene las bases de datos de usuario que participa en el AG. Los datos de configuración se envían de forma sincrónica desde el servidor principal. Estos datos de configuración, a continuación, se usan durante las conmutaciones por error, independientemente de si están automático o manual.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-extract-transform-and-load-data-on-linux-with-ssissql-server-linux-migrate-ssismd"></a>2. &nbsp;[Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

*Actualizado: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1))

<!-- Source markdown line 50.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9bba002ae3955ebb8376c7c85b7ec1ac8c706073 1533a8e0bfe553e5404de79129119b3f93185ee9  (PR=4768  ,  Filename=sql-server-linux-migrate-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  Especifique el `/de[crypt]` opción para especificar la contraseña de forma interactiva, tal como se muestra en el ejemplo siguiente:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de

    Enter decryption password:
    ```

3.  Especifique el `/de` opción para proporcionar la contraseña en la línea de comandos, tal como se muestra en el ejemplo siguiente. Este método no se recomienda ya que almacena la contraseña de descifrado con el comando del historial de comandos.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test

    Warning: Using /De[crypt] <password> may store decryption password in command history.

    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

**Diseñar paquetes**


**Conectarse a orígenes de datos ODBC**. Con SSIS al actualizar los Linux CTP 2.1 y versiones posteriores, paquetes SSIS pueden usar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el servidor SQL Server y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador de ODBC Unicode que se ajusta a la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede utilizar la autenticación de Windows. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).







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
- [Nuevos y actualizados (0 + 0): **ActiveX Data Objects (ADO) para SQL** documentos](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (0 + 0): **ejemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)


