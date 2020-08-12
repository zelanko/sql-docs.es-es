---
title: Crear una consulta en el Diseñador de consultas relacionales (Generador de informes y SSRS)
description: Obtenga información sobre cómo crear una consulta en el Diseñador de consultas relacionales para que pueda especificar qué datos se deben recuperar de un origen de datos externo para un conjunto de datos de informe.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 04/25/2019
ms.openlocfilehash: 5ead07a1cf2afa13189b76c0c6eb75a472699543
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85808485"
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Crear una consulta en el Diseñador de consultas relacionales (Generador de informes y SSRS)

Los diseñadores de consultas le ayudan a especificar los datos que se deben recuperar de un origen de datos externo para un conjunto de datos de informe. Puede utilizar un diseñador de consultas cuando genere una consulta en un asistente o cree una consulta de conjunto de datos.  
  
> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Una conjunto de datos se basa en un origen de datos. El tipo de origen de datos y el entorno de creación determina el diseñador de consultas que se ha de abrir al definir la consulta de conjunto de datos. Las características del diseñador de consultas varían en función del origen de datos subyacente. Para más información sobre capas de datos, vea [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).

 Puede utilizar un diseñador de consultas para las siguientes tareas:  
  
-   Explorar los metadatos de varios esquemas en el origen de datos externo  
  
-   Especificar los campos para recuperar del conjunto de datos  
  
-   Especificar las relaciones entre dos objetos, como las tablas  
  
-   Especificar filtros para restringir los datos antes de recuperarlos como datos del informe  
  
-   Indicar si se crearán parámetros  
  
-   Especificar agregados para realizar cálculos en el origen de datos externo  
  
 Después de abrir un diseñador de consultas, cree una consulta de la misma manera para un conjunto de datos incrustado que para uno compartido. Los siguientes procedimientos utilizan una consulta de conjunto de datos incrustada.  
  
 Para obtener más información, vea [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md).  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>Para crear una consulta para un conjunto de datos incrustado en la vista de diseño del informe  
  
1.  Abra el diseñador de consultas. En el panel Datos de informe, haga clic con el botón derecho en el conjunto de datos y, después, haga clic en **Consulta**.  
  
     Se abrirá el diseñador de consultas que esté asociado al origen de datos compartido.  
  
2.  En el panel Vista de base de datos, expanda las carpetas que muestran una vista jerárquica de objetos de esquema de la base de datos, como tablas, vistas y procedimientos almacenados. Haga clic en el cuadro de selección para elegir todos los campos de un objeto o expandir el nodo para seleccionar campos individuales.  
  
     A medida que seleccione campos en el panel Vista de base de datos, el panel **Seleccionar campos** mostrará sus selecciones.  
  
     Si selecciona campos de más de una tabla de base de datos relacionada, utilice el panel Relaciones para ver las relaciones entre tablas que se detectaron en el esquema de la base de datos.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     La lista de campos de conjunto de datos aparecerá en el panel Datos de informe.  
  
### <a name="to-specify-limits-for-a-query"></a>Para especificar los límites de una consulta  
  
1.  En el diseñador de consultas relacionales, compruebe que los campos están seleccionados y que aparecen en el panel **Campos seleccionados** .  
  
2.  En la barra de herramientas del panel Filtros aplicados, haga clic en **Agregar filtro**. Aparece una nueva fila de filtro.  
  
3.  En **Nombre de campo**, haga clic para mostrar la lista desplegable de campos y, después, haga clic en el nombre del campo por el que quiere filtrar. Por ejemplo, para filtrar por cantidad, haga clic en el campo que contiene el número de elementos.  
  
4.  En **Operador**, haga clic para mostrar la lista desplegable de operadores y, después, seleccione el operador de comparación que se usará en el filtro.  
  
5.  En **Valor**, escriba el valor por el que desea filtrar. Por ejemplo, para filtrar por una cantidad mayor que 100, escriba 100.  
  
6.  Seleccione la opción de parámetro de esta fila para crear un parámetro de conjunto de datos que permita a los usuarios especificar valores de filtro. Automáticamente se creará un parámetro de informe que coincida con el parámetro de conjunto de datos.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 La lista de campos de conjunto de datos aparecerá en el panel Datos de informe.  
  
### <a name="to-view-a-query-result-set"></a>Para ver un conjunto de resultados de consulta  
  
1.  En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar consulta (!)** .  
  
    > [!NOTE]  
    >  El diseñador de consultas utiliza las credenciales de tiempo de diseño para ejecutar la consulta y recuperar el conjunto de resultados. Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](specify-credential-and-connection-information-for-report-data-sources.md).  
  
 La consulta se ejecuta en el origen de datos y devuelve datos de ejemplo en el panel Resultados de la consulta.  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [Herramientas de diseño de consulta &#40;SSRS&#41;](query-design-tools-ssrs.md)   
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Vista de diseño de informe &#40;Generador de informes&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Vista de diseño de conjunto de datos compartidos &#40;Generador de informes&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Diseñadores de consultas de Reporting Services](https://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)  
  
  
