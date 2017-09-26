---
title: "Cuadro de diálogo (importación de SQL Server y el Asistente para exportación) de detalles de conversión de columna | Documentos de Microsoft"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 985ba8a478999a153b3bb32649b98c3e809fc5e8
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Cuadro de diálogo Detalles de conversión de columna (Asistente para importación y exportación de SQL Server)
  Si hace doble clic en la fila de una columna individual de la página **Revisar asignación de tipos de datos** , el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abrirá el cuadro de diálogo **Detalles de conversión de columna** . En esta página, puede revisar información detallada sobre la conversión de una columna individual. En la información se incluyen los siguientes elementos.
-   El tipo de datos de la columna en el origen y el destino.
-   El tipo de datos conversión que realizará el asistente, si se requiere la conversión.
-   Los archivos de asignación de tipos de datos que usa el asistente para determinar la conversión de tipos de datos necesaria. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Captura de pantalla de la página Detalles de conversión de columna 
 En la captura de pantalla siguiente se muestra el cuadro de diálogo **Detalles de conversión de columna** del asistente después de que el usuario haya hecho doble clic en una fila de la página **Revisar asignación de tipos de datos** . Para volver a ver la página **Revisar asignación de tipos de datos** , vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
En este ejemplo, verá lo siguiente.
-   El `PersonID` columna en la tabla de SQL Server de origen es de tipo `int`. El asistente asigna este tipo para SQL Server Integration Services (SSIS) `DT_I4` tipo de datos, que es un entero con signo de cuatro bytes, haciendo referencia al archivo de asignación de tipo de datos MSSQLToSSIS10.xml.
-   El `PersonID` columna en la tabla de SQL Server de destino también es de tipo `int`. El asistente asigna este tipo para el mismo tipo de datos SSIS.
-   El asistente finaliza, *esta columna no necesita conversión*.
 
  
 ![Página de conversión de columna de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/column-conversion.png "página de conversión de columna de la importación y el Asistente para exportación") 
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de revisar los detalles de la conversión de columna y de hacer clic en **Aceptar**, el cuadro de diálogo **Detalles de conversión de columna** le volverá a dirigir a la página **Revisar asignación de tipos de datos** . Para más información, vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

