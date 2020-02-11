---
title: Evaluar objetos de base de datos de Access para la conversión (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 4c2f5bc6953ab0e96397ca728391cbe22a73dd50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910691"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>Evaluar objetos de base de datos de Access para la conversión (AccessToSQL)
Antes de cargar objetos y migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, debe determinar la cantidad de la migración que se realizará correctamente y el tiempo que puede tardar la conversión. SSMA puede crear un informe de evaluación que muestre el porcentaje de objetos que se convirtieron [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correctamente en o SQL Azure la sintaxis y estimaciones de tiempo para realizar la migración. SSMA también le permite ver los problemas específicos que provocaron errores de conversión.  
  
## <a name="creating-assessment-reports"></a>Creación de informes de evaluación  
Cuando crea un informe de evaluación, SSMA convierte los objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access seleccionados en sintaxis o SQL Azure y, a continuación, muestra los resultados.  
  
**Para crear un informe de evaluación**  
  
1.  En el explorador de metadatos de Access, seleccione las bases de datos que desea evaluar.  
  
2.  Para omitir los objetos individuales, desactive las casillas situadas junto a los objetos que no desea evaluar.  
  
3.  Haga clic con el botón derecho en **bases de datos**y, a continuación, seleccione **crear informe**.  
  
    También puede analizar objetos individuales haciendo clic con el botón secundario en un objeto y, a continuación, seleccionando **crear informe**.  
  
    SSMA muestra el progreso en la barra de estado en la parte inferior de la ventana. Si el panel de salida está visible, también verá mensajes en el panel de salida.  
  
Una vez completada la evaluación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecerá la ventana Migration Assistant de acceso: informe de evaluación.  
  
## <a name="using-assessment-reports"></a>Uso de informes de evaluación  
La ventana Informe de evaluación contiene tres paneles: un explorador, un panel de detalles y un panel de mensajes.  
  
-   El panel explorador permite examinar los objetos que se han evaluado. Puede hacer clic en los elementos de este panel para explorar en profundidad tablas, índices y claves individuales.  
  
-   En el panel de detalles se muestran las estadísticas de conversión del objeto seleccionado.  
  
-   En el panel de mensajes se muestran los errores, las advertencias y los mensajes informativos para la conversión y las estimaciones de tiempo para realizar la migración y los pasos de corrección de errores individuales.  
  
Debe corregir los errores antes de volver a ejecutar el informe de evaluación o convertir los esquemas. Para buscar errores, haga clic en el botón **errores** en el panel mensajes y, a continuación, expanda cada error para ver una lista de los objetos en los que se produjo el error. Si hace clic en un objeto en el panel mensajes, todos los errores y advertencias de ese objeto aparecerán en el panel de detalles.  
  
## <a name="next-step"></a>siguiente paso  
[Conversión de objetos de base de datos de Access](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
