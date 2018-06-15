---
title: 'Actualizado: los documentos de las operaciones de SQL Studio | Documentos de Microsoft'
description: Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, las operaciones de SQL Studio.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssops
ms.date: 04/28/2018
ms.openlocfilehash: 074ed6176480655d9d87a55eb87cbb76b3011b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32686525"
---
# <a name="new-and-recently-updated-sql-operations-studio-docs"></a>Las nuevas y recientemente actualizado: los documentos de las operaciones de SQL Studio



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2018-02-03** &nbsp; - a - &nbsp; **2018-04-28**
- *Área de asunto:* &nbsp; **Studio de operaciones SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


- [Ampliar la funcionalidad de las operaciones de SQL Studio (versión preliminar)](extensions.md)

<!-- GeneMi:  I MANUALLY replace the ugly !INCLUDE with the name from inside the includes file. -->


&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Descargue e instale las operaciones de SQL Studio (versión preliminar)](#TitleNum_1)
2. [Notas de la versión de las operaciones de SQL Studio (versión preliminar)](#TitleNum_2)
3. [Tutorial: Agregar la *cinco consultas más lentas* widget de ejemplo en el panel de la base de datos](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-and-install-sql-operations-studio-previewdownloadmd"></a>1. &nbsp; [Descargue e instale las operaciones de SQL Studio (versión preliminar)](download.md)

*Actualizado: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 64.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6b4f80ad54c599e4354303a736f62e9715f99a32 18b22f464bbd8676348248ba5717b71acbab1c0d  (PR=5676  ,  Filename=download.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



   **Instalación de Debian:**
```
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
```

   **Instalación de RPM:**
```
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
```

   **TAR.gz instalación:**



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-operations-studio-preview-release-notesrelease-notesmd"></a>2. &nbsp; [Notas de la versión de las operaciones de SQL Studio (versión preliminar)](release-notes.md)

*Actualizado: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e2901d8a197f375f7d10ec93cbc9320362bf9278 0dde1aceceb339cb4cacd744e469f3d85d589668  (PR=5676  ,  Filename=release-notes.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[Descargar la versión preliminar pública de abril]**


**Abril de 2018 (versión preliminar pública de abril)**


fecha de lanzamiento: versión 25 de abril de 2018: 0.28.6

El *abril Public Preview* contiene mejoras y correcciones de errores.

- Mejoras en la extensión de la versión preliminar del Agente SQL.
- Grandes y protegido el archivo compatibilidad mejorada para guardar administrador protegida y > 256M archivos dentro de las operaciones de SQL Studio.
- Integra la división de Terminal para trabajar con varias terminales abiertos al mismo tiempo.
- Imprimir en el pie de recuento de archivo en disco de instalación reducido para instalaciones más rápidas y tiempos de inicio.
- Seguir solucionar problemas de GitHub:
   - Corregir [emitir 37](https://github.com/Microsoft/sqlopsstudio/issues/37): cuando el Visor gráfico produce un error, se produce un comportamiento inesperado.
   - Corregir [emitir 462](https://github.com/Microsoft/sqlopsstudio/issues/462): solicitud de característica: opción para grupos de servidores se expanda de forma predeterminada.
   - Corregir [emitir 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense - propuesta no válida para el comando 'update'.
   - Corregir [emitir 967](https://github.com/Microsoft/sqlopsstudio/issues/967): esperar que el plan de consulta cuando selecciona el plan de presentación XML en la cuadrícula de resultados.
   - Corregir [emitir 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): agregar corchetes para llamada ms_foreachdb desde flyfishingdba.
   - Corregir [emitir 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): error de protocolo de enlace de inicio de sesión previo SSL/TLS.
   - Corregir [emitir 1050](https://github.com/Microsoft/sqlopsstudio/issues/1050): visión clara ver antes de mostrar el error.
   - Corregir [emitir 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): nuevas acciones de consulta en el Explorador de widget y restauración se interrumpen.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboardtutorial-qds-sql-servermd"></a>3. &nbsp; [Tutorial: Agregar la *cinco consultas más lentas* widget de ejemplo en el panel de la base de datos](tutorial-qds-sql-server.md)

*Actualizado: 2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2))

<!-- Source markdown line 94.  ms.author= "erickang".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bc128acd966898cafc04381d7d83187d28466052 a47bf93ea4165618e0e514d7900ce1461f691aae  (PR=5676  ,  Filename=tutorial-qds-sql-server.md  ,  Dirpath=docs\sql-operations-studio\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (11 + 6): &nbsp; &nbsp; **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (18 + 0): &nbsp; &nbsp; **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (218 + 14): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (14 + 0): &nbsp; &nbsp; **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (3 + 2): &nbsp; &nbsp; **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (3 + 3): &nbsp; &nbsp; **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (10 + 7): &nbsp; &nbsp; **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (0 + 2): &nbsp; &nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (1 + 3): &nbsp; &nbsp; **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2): &nbsp; &nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Nuevos y actualizados (1 + 1): &nbsp; &nbsp; **Tools para SQL** documentos](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (0 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Nuevos y actualizados (0 + 0): **ejemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)

