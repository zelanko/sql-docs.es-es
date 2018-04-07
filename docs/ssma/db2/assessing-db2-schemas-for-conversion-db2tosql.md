---
title: Evaluar los esquemas de DB2 para la conversión (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
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
ms.assetid: 8892f5a4-72ba-4406-8649-7a9d67f4c1d9
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96c437f34bbe4b45c33082a18536aef33dd4b218
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="assessing-db2-schemas-for-conversion-db2tosql"></a>Evaluar los esquemas de DB2 para la conversión (DB2ToSQL)
Antes de cargar los objetos y migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], debe determinar cómo compleja será la migración y cuánto tiempo tardará la migración. SSMA puede crear un informe de evaluación que muestra el porcentaje de los objetos que se convertirán correctamente. SSMA también le permite ver los problemas específicos que dar lugar a errores de conversión.  
  
## <a name="creating-assessment-reports"></a>Creación de informes de evaluación  
Al crear este informe de evaluación, SSMA convierte los objetos de base de datos de DB2 seleccionados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis y, a continuación, muestra los resultados.  
  
**Para crear un informe de evaluación**  
  
1.  En el Explorador de metadatos de DB2, seleccione los esquemas que se va a evaluar.  
  
2.  Para omitir los objetos individuales, desactive las casillas de verificación situadas junto a los.  
  
3.  Haga clic en **esquemas**y, a continuación, seleccione **crear informe**.  
  
    También puede analizar los objetos individuales haciendo clic en un objeto y, a continuación, seleccione **crear informe**.  
  
    SSMA mostrará el progreso de la barra de estado en la parte inferior de la ventana. Si está visible el panel de resultados, también verá mensajes en el panel de resultados.  
  
    Una vez completada, la evaluación de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para DB2: aparecerá la ventana de informe de evaluación.  
  
## <a name="using-assessment-reports"></a>Uso de informes de evaluación  
La ventana de informe de evaluación contiene tres paneles:  
  
-   El panel izquierdo contiene la jerarquía de objetos que se incluyen en el informe de evaluación. Puede examinar la jerarquía y seleccionar objetos y las categorías de objetos para ver el código y las estadísticas de la conversión.  
  
-   El contenido del panel derecho depende el elemento que está seleccionado en el panel izquierdo.  
  
    Si se selecciona un grupo de objetos, un esquema de este tipo, o si se selecciona una tabla, el panel derecho contiene un panel de estadísticas de conversión y objetos de un panel de categorías. El panel de estadísticas de conversión muestra las estadísticas de conversión para los objetos seleccionados. Los objetos de panel de categorías muestra las estadísticas de conversión para el objeto o categorías de objetos.  
  
    Si se selecciona una función, paquete, procedimiento, secuencia o vista, el panel derecho contiene estadísticas, el código fuente y el código de destino.  
  
    -   El área superior muestra las estadísticas generales para el objeto. Es posible que tengas que expandir **estadísticas** para ver esta información.  
  
    -   El área de origen muestra el código fuente del objeto seleccionado en el panel izquierdo. Las áreas resaltadas mostrar código fuente problemático.  
  
    -   El área de destino muestra el código convertido. Texto rojo y muestra los mensajes de error y de código problemáticos.  
  
-   El panel inferior muestra los mensajes de conversión, agrupados por número de mensaje. Puede hacer clic en **errores**, **advertencias**, o **información** para ver las categorías de mensajes y, a continuación, expanda un grupo de mensajes. Haga clic en un mensaje individual puede seleccionar el objeto en el panel izquierdo y mostrar los detalles en el panel derecho.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>Analizar problemas de conversión mediante el informe de evaluación  
El panel de estadísticas de conversión muestra las estadísticas de conversión. Si el porcentaje de cualquier categoría es inferior a 100%, debe determinar por qué la conversión no tuvo éxito.  
  
**Para ver los problemas de conversión**  
  
1.  Crear el informe de evaluación mediante el uso de las instrucciones que aparecen en el procedimiento anterior.  
  
2.  En el panel izquierdo, expanda esquemas o carpetas que tienen un icono rojo de error. Continúe expandiendo los elementos hasta que haya seleccionado un elemento individual que no se pudo conversión.  
  
3.  En la parte superior del panel de origen, haga clic en **problema siguiente**.  
  
    Se resalta el código problemático, como es el código relacionado en el panel de navegación de destino.  
  
4.  Revise los mensajes de error y, a continuación, determine qué desea hacer con el objeto que produjo el problema de conversión:  
  
    -   Actualizar la sintaxis de DB2 en SSMA. Puede actualizar la sintaxis de procedimientos, funciones, desencadenadores, funciones empaquetadas y procedimientos empaquetados. Para actualizar la sintaxis, seleccione el objeto en el panel del explorador de metadatos de DB2, haga clic en el **SQL** ficha y, a continuación, modifique el código SQL. Si mientras navega sale del elemento, deberá guardar la sintaxis actualizada. También puede ver los errores para el objeto en el **informe** ficha.  
  
    -   En DB2, puede modificar el objeto de DB2 para quitar o revisar cargue código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectarse a la base de datos DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
    -   Puede excluir el objeto de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos y el Explorador de metadatos de DB2, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y migrar datos de DB2.  
  
## <a name="next-step"></a>Paso siguiente  
[Convertir esquemas de DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de DB2 migrar a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
