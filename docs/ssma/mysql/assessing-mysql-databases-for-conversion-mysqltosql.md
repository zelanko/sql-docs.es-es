---
title: Evaluar las bases de datos de MySQL para la conversión (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13035f6ca6e0a2dc95b3b0f7907b066abdbda716
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>Evaluar las bases de datos de MySQL para la conversión (MySQLToSQL)
Antes de cargar los objetos y migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, debe determinar cómo compleja será la migración y cuánto tiempo tardará la migración. SSMA puede crear un informe de evaluación que muestra el porcentaje de los objetos que se convertirán correctamente. SSMA también le permite ver los problemas específicos que dar lugar a errores de conversión.  
  
## <a name="creating-assessment-reports"></a>Creación de informes de evaluación  
Al crear este informe de evaluación, SSMA convierte los objetos seleccionados de base de datos de MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o sintaxis de SQL Azure y, a continuación, muestra los resultados.  
  
**Para crear un informe de evaluación**  
  
1.  En el Explorador de metadatos de MySQL, seleccione los esquemas que se va a evaluar.  
  
2.  Para omitir los objetos individuales, desactive las casillas de verificación situadas junto a los.  
  
3.  Haga clic en **esquemas**y, a continuación, seleccione **crear informe**.  
  
    Haga clic en un objeto para analizar objetos individuales. A continuación, seleccione **crear informe**.  
  
    SSMA mostrará el progreso de la barra de estado en la parte inferior de la ventana. Si está visible el panel de resultados, también verá mensajes en el panel de resultados.  
  
    Una vez completada, la evaluación de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para MySQL, ventana de informe de evaluación se mostrarán.  
  
## <a name="using-assessment-reports"></a>Uso de informes de evaluación  
La ventana de informe de evaluación contiene tres paneles:  
  
-   El panel izquierdo contiene la jerarquía de objetos que se incluyen en el informe de evaluación. Puede examinar la jerarquía y seleccionar objetos y las categorías de objetos para ver el código y las estadísticas de la conversión.  
  
-   El contenido del panel derecho depende el elemento que está seleccionado en el panel izquierdo.  
  
    Si se selecciona un grupo de objetos, como el esquema, el panel derecho contiene un panel de estadísticas de conversión y objetos mediante el panel de categorías. El panel de estadísticas de conversión muestra las estadísticas de conversión para los objetos seleccionados. Los objetos de panel de categorías muestra las estadísticas de conversión para el objeto o categorías de objetos.  
  
    Si se selecciona una función, procedimiento, tabla o vista, el panel derecho contiene estadísticas, el código fuente y el código de destino.  
  
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
  
4.  Revise los mensajes de error y, a continuación, determine qué desea hacer con el objeto que produjo el problema de conversión.  
  
-   Actualizar la sintaxis de MySQL de SSMA. Puede actualizar la sintaxis solo para los procedimientos y funciones. Para actualizar la sintaxis, seleccione el objeto en el panel del explorador de metadatos de MySQL, haga clic en el **SQL** ficha y, a continuación, modifique el código SQL. Si mientras navega sale del elemento, deberá guardar la sintaxis actualizada. También puede ver los errores para el objeto en el **informe** ficha.  
  
-   En MySQL, puede modificar el objeto de MySQL para quitar o revisar cargue código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   Puede excluir el objeto de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure y el Explorador de metadatos de MySQL, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure y migrar datos de MySQL.  
  
## <a name="next-step"></a>Paso siguiente  
[Conversión de bases de datos MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
