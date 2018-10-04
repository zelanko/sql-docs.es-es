---
title: Proporcionar una consulta de origen (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3abb49fa9e2e73ae5c610b5e940a6deba5079d62
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069865"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Proporcionar una consulta de origen (Asistente para importación y exportación de SQL Server)
  Use la **proporcionar una consulta de origen** página para escribir la instrucción SQL que generará los datos que se va a copiar desde el origen de datos al destino.  
  
 Para más información acerca de este asistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información acerca de las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Instrucción SQL**  
 Escriba una instrucción de consulta para recuperar las filas de datos seleccionadas de la base de datos de origen. Por ejemplo, la siguiente instrucción de consulta recupera **SalesPersonID**, **SalesQuota**y **SalesYTD** de la base de datos AdventureWorks para los vendedores con un porcentaje de comisión superior al 1,5%.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **Analizar**  
 Comprueba la sintaxis de la instrucción SQL en el cuadro de texto **Instrucción SQL**.  
  
> [!NOTE]  
>  Si el tiempo necesario para comprobar la sintaxis de la instrucción supera el valor de tiempo de espera de 30 segundos, el análisis se detiene y se genera un error. No podrá pasar esta página del asistente hasta que el análisis se realice correctamente. Una solución es crear una vista de base de datos basada en la consulta y consultar la vista del asistente, en lugar de escribir directamente el texto de la consulta.  
  
 **Examinar**  
 Seleccione un archivo que contiene una instrucción SQL mediante el uso de la **abierto** cuadro de diálogo. Al seleccionar un archivo se copiará el texto del archivo en el cuadro de texto **Instrucción de consulta** .  
  
  
