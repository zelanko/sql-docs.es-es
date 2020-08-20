---
description: Cuadro de diálogo Detalles de conversión de columna (Asistente para importación y exportación de SQL Server)
title: Cuadro de diálogo Detalles de conversión de columna (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 18e512c1834a74be5c45ce81fd859eaebb375be5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484158"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Cuadro de diálogo Detalles de conversión de columna (Asistente para importación y exportación de SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Si hace doble clic en la fila de una columna individual de la página **Revisar asignación de tipos de datos** , el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abrirá el cuadro de diálogo **Detalles de conversión de columna** . En esta página, puede revisar información detallada sobre la conversión de una columna individual. En la información se incluyen los siguientes elementos.
-   El tipo de datos de la columna en el origen y en el destino.
-   La conversión del tipo de datos que realizará el asistente, si se necesita una.
-   Los archivos de asignación de tipos de datos que usa el asistente para determinar la conversión de tipos de datos necesaria. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Captura de pantalla de la página Detalles de conversión de columna 
 En la captura de pantalla siguiente se muestra el cuadro de diálogo **Detalles de conversión de columna** del asistente después de que el usuario haya hecho doble clic en una fila de la página **Revisar asignación de tipos de datos** . Para volver a ver la página **Revisar asignación de tipos de datos** , vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
En este ejemplo, puede ver lo siguiente.
-   La columna `PersonID` en la tabla de SQL Server de origen es de tipo `int`. El asistente asigna este tipo al tipo de datos `DT_I4` de SQL Server Integration Services (SSIS), que es un entero con signo de cuatro bytes, haciendo referencia al archivo de asignación de tipos de datos MSSQLToSSIS10.xml.
-   La columna `PersonID` en la tabla de SQL Server de destino también es de tipo `int`. El asistente asigna este tipo al mismo tipo de datos de SSIS.
-   El asistente finaliza con el mensaje *Esta columna no necesita conversión*.
 
  
 ![Página de conversión de columnas del Asistente para importar y exportar](../../integration-services/import-export-data/media/column-conversion.png "Página de conversión de columnas del Asistente para importar y exportar") 
  
## <a name="whats-next"></a>A continuación  
 Después de revisar los detalles de la conversión de columna y de hacer clic en **Aceptar**, el cuadro de diálogo **Detalles de conversión de columna** le volverá a dirigir a la página **Revisar asignación de tipos de datos** . Para más información, vea [Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
