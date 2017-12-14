---
title: "Cuadro de diálogo Detalles de conversión de columna (Asistente para importación y exportación de SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81ff6011b40700f75dba019356e3c0d80e94f969
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Cuadro de diálogo Detalles de conversión de columna (Asistente para importación y exportación de SQL Server)
  Si hace doble clic en la fila de una columna individual de la página **Revisar asignación de tipos de datos** , el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abrirá el cuadro de diálogo **Detalles de conversión de columna** . En esta página, puede revisar información detallada sobre la conversión de una columna individual. En la información se incluyen los siguientes elementos.
-   El tipo de datos de la columna en el origen y en el destino.
-   La conversión del tipo de datos que realizará el asistente, si se necesita una.
-   Los archivos de asignación de tipos de datos que usa el asistente para determinar la conversión de tipos de datos necesaria. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Captura de pantalla de la página Detalles de conversión de columna 
 En la captura de pantalla siguiente se muestra el cuadro de diálogo **Detalles de conversión de columna** del asistente después de que el usuario haya hecho doble clic en una fila de la página **Revisar asignación de tipos de datos** . Para volver a ver la página **Revisar asignación de tipos de datos** , vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
En este ejemplo, puede ver lo siguiente.
-   La columna `PersonID` en la tabla de SQL Server de origen es de tipo `int`. El asistente asigna este tipo al tipo de datos `DT_I4` de SQL Server Integration Services (SSIS), que es un entero con signo de cuatro bytes, haciendo referencia al archivo de asignación de tipos de datos MSSQLToSSIS10.xml.
-   La columna `PersonID` en la tabla de SQL Server de destino también es de tipo `int`. El asistente asigna este tipo para el mismo tipo de datos de SSIS.
-   El asistente finaliza con el mensaje *Esta columna no necesita conversión*.
 
  
 ![Página de conversión de columnas del Asistente para importación y exportación](../../integration-services/import-export-data/media/column-conversion.png "Column conversion page of the Import and Export Wizard") 
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de revisar los detalles de la conversión de columna y de hacer clic en **Aceptar**, el cuadro de diálogo **Detalles de conversión de columna** le volverá a dirigir a la página **Revisar asignación de tipos de datos** . Para más información, vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
