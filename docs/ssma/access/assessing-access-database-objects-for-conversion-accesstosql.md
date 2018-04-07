---
title: Evaluar los objetos de base de datos de acceso para la conversión (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f34d6d2c90b90a5afc7b10a19cc5d82373a26a86
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>Evaluar los objetos de base de datos de acceso para la conversión (AccessToSQL)
Antes de cargar los objetos y migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, debe determinar la cantidad de la migración se realice correctamente, y cuánto tiempo tardará la conversión. SSMA puede crear un informe de evaluación que muestra el porcentaje de los objetos que se han convertido correctamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o estimaciones de tiempo y la sintaxis de SQL Azure para llevar a cabo la migración. SSMA también le permite ver los problemas específicos que produjeron errores de conversión.  
  
## <a name="creating-assessment-reports"></a>Creación de informes de evaluación  
Cuando crea un informe de evaluación, SSMA convierte los objetos seleccionados de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o sintaxis de SQL Azure y, a continuación, muestra los resultados.  
  
**Para crear un informe de evaluación**  
  
1.  En el Explorador de metadatos de acceso, seleccione la base de datos o bases de datos que se desea evaluar.  
  
2.  Para omitir los objetos individuales, desactive las casillas de verificación junto a los objetos que no desea evaluar.  
  
3.  Haga clic en **bases de datos**y, a continuación, seleccione **crear informe**.  
  
    También puede analizar los objetos individuales haciendo clic en un objeto y, a continuación, seleccione **crear informe**.  
  
    SSMA muestra el progreso en la barra de estado en la parte inferior de la ventana. Si está visible el panel de resultados, también verá mensajes en el panel de resultados.  
  
Una vez completada, la evaluación de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Access: aparecerá la ventana de informe de evaluación.  
  
## <a name="using-assessment-reports"></a>Uso de informes de evaluación  
La ventana de informe de evaluación contiene tres paneles: un explorador, un panel de detalles y un panel de mensajes.  
  
-   El panel de exploración permite examinar los objetos que se evaluaron. Puede hacer clic en elementos de este panel para examinar con detalle las claves, índices y tablas individuales.  
  
-   El panel de detalles muestra las estadísticas de conversión para el objeto seleccionado.  
  
-   El panel de mensajes muestra los errores, advertencias y mensajes informativos de la conversión y estimaciones de tiempo para realizar la migración y pasos de corrección de errores individuales.  
  
Debe corregir los errores antes de volver a ejecutar el informe de evaluación o convertir esquemas. Para buscar errores, haga clic en el **errores** situado en el panel de mensajes y, a continuación, expanda cada error para ver una lista de objetos donde se produjo el error. Si hace clic en un objeto en el panel de mensajes, todos los errores y advertencias para ese objeto aparecerá en el panel de detalles.  
  
## <a name="next-step"></a>Paso siguiente  
[Conversión de objetos de base de datos de Access](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
