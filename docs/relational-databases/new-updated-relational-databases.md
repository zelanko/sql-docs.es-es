---
title: 'Actualizados: documentos de bases de datos relacionales | Microsoft Docs'
description: "Muestra fragmentos del contenido actualizado en la documentación de bases de datos relacionales que ha cambiado recientemente."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: ee7d66bcd8720234f4aec97d24ce16ed21888a3c
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Nuevos y actualizados recientemente: documentos de bases de datos relacionales



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* del &nbsp; **18-07-2017** &nbsp; al &nbsp; **11-09-2017**
- *Área temática:* &nbsp; **Bases de datos relacionales**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Importación de datos de Excel a SQL Server o Azure SQL Database](import-export/import-data-from-excel-to-sql.md)
2. [Solución de problemas de conectividad de Kerberos con PolyBase](polybase/polybase-troubleshoot-connectivity.md)
3. [Cifrado de datos transparente (TDE)](security/encryption/transparent-data-encryption.md)
4. [Cifrado de datos transparente para Azure SQL Database y Data Warehouse](security/encryption/transparent-data-encryption-azure-sql.md)
5. [Cifrado de datos transparente compatible con Bring Your Own Key para Azure SQL Database y SQL Data Warehouse](security/encryption/transparent-data-encryption-byok-azure-sql.md)
6. [PowerShell: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)
7. [Girar el protector del Cifrado de datos transparente (TDE) mediante PowerShell](security/encryption/transparent-data-encryption-byok-azure-sql-key-rotation.md)
8. [Eliminación de un protector de cifrado de datos transparente (TDE) mediante PowerShell](security/encryption/transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)
9. [Términos de licencia de los objetos de administración compartida (SMO) de SQL Server](server-management-objects-smo/smo-license-terms.md)
10. [sys.external_libraries (Transact-SQL)](system-catalog-views/sys-external-libraries-transact-sql.md)
11. [sys.external_library_files (Transact-SQL)](system-catalog-views/sys-external-library-files-transact-sql.md)
12. [sp_rxPredict](system-stored-procedures/sp-rxpredict-transact-sql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Ajuste automático](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-automatic-tuningautomatic-tuningautomatic-tuningmd"></a>1. &nbsp; [Ajuste automático](automatic-tuning/automatic-tuning.md)

*Actualizado: 16-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 64.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 be765a1acf9bdfd5485520d16160677583e81f8e 135d926227094374e6ec5484e7babee625b44bb2  (PR=2860  ,  Filename=automatic-tuning.md  ,  Dirpath=docs\relational-databases\automatic-tuning\  ,  MergeCommitSha40=e4a6157cb56c6db911406585f841046a431eef99) -->



**Corrección automática de la elección del plan**


..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] puede cambiar automáticamente al último plan bueno conocido siempre que se detecta la regresión de la elección del plan.

![SQL plan choice correction--media/force-last-good-plan.png "SQL plan choice correction")

..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] detecta automáticamente cualquier regresión posible de elección del plan, incluido el plan que se debe usar en lugar del plan incorrecto.
Cuando el ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] aplica el último plan bueno conocido, supervisa automáticamente el rendimiento del plan forzado. Si el plan forzado no es mejor que el plan con regresión, el nuevo plan no será forzado y el ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] compilará un nuevo plan. Si ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] comprueba que el plan forzado es mejor que el plan con regresión, el plan forzado se conservará hasta que se produzca una nueva compilación (por ejemplo, en el próximo cambio de esquema o de estadísticas) si es mejor que el plan con regresión.

**Habilitar la corrección automática de la elección del plan**


Puede habilitar el ajuste automático por base de datos y especificar que se debería forzar el último plan bueno siempre que se detecte alguna regresión de cambio de plan. El ajuste automático se habilita con el siguiente comando:

```
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON );
```
Una vez activada esta opción, ..!NCLUDE-NotShown--ssde_md--../../includes/ssde_md.md)] forzará automáticamente cualquier recomendación en la que la ganancia de CPU estimada sea superior a 10 segundos, o el número de errores del nuevo plan sea mayor que el número de errores del plan recomendado, y comprobará que el plan forzado es mejor que el actual.

**Alternativa: corrección manual de elección del plan**


Sin el ajuste automático, los usuarios deberán supervisar el sistema de forma periódica y buscar las consultas con regresión. Si alguno de los planes tuvo regresión, el usuario debería encontrarlo.







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (3+12): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (5+0): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (5+1): documentos de **Motor de base de datos para SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (19+82): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (1+8): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (12+1): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (0+1): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (7+1): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (1+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (0+2): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (1+4): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (4+1): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Nuevos + actualizados (0+1): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)



