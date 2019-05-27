---
title: Crear una consulta en el Diseñador de consultas relacionales (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 901abf5be70f0b3c70b89b0415c59f19a9327b29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107436"
---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Crear una consulta en el Diseñador de consultas relacionales (Generador de informes y SSRS)
  Los diseñadores de consultas le ayudan a especificar los datos que se deben recuperar de un origen de datos externo para un conjunto de datos de informe. Puede utilizar un diseñador de consultas cuando genere una consulta en un asistente o cree una consulta de conjunto de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Una conjunto de datos se basa en un origen de datos. El tipo de origen de datos y el entorno de creación determina el diseñador de consultas que se ha de abrir al definir la consulta de conjunto de datos. Las características del diseñador de consultas varían en función del origen de datos subyacente. Para obtener más información acerca de las capas de datos, vea [conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md) o [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) .  
  
 Puede utilizar un diseñador de consultas para las siguientes tareas:  
  
-   Explorar los metadatos de varios esquemas en el origen de datos externo  
  
-   Especificar los campos para recuperar del conjunto de datos  
  
-   Especificar las relaciones entre dos objetos, como las tablas  
  
-   Especificar filtros para restringir los datos antes de recuperarlos como datos del informe  
  
-   Indicar si se crearán parámetros  
  
-   Especificar agregados para realizar cálculos en el origen de datos externo  
  
 Después de abrir un diseñador de consultas, cree una consulta de la misma manera para un conjunto de datos incrustado que para uno compartido. Los siguientes procedimientos utilizan una consulta de conjunto de datos incrustada.  
  
 Para obtener más información, vea [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](relational-query-designer-user-interface-report-builder.md).  
  
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
  
1.  En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar consulta (!)**.  
  
    > [!NOTE]  
    >  El diseñador de consultas utiliza las credenciales de tiempo de diseño para ejecutar la consulta y recuperar el conjunto de resultados. Para más información, vea [Especificar credenciales en el Generador de informes](../specify-credentials-in-report-builder.md).  
  
 La consulta se ejecuta en el origen de datos y devuelve datos de ejemplo en el panel Resultados de la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)   
 [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)   
 [Diseñadores de consultas &#40;Generador de informes&#41;](../query-designers-report-builder.md)   
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Vista de diseño de informe &#40;Generador de informes&#41;](../report-builder/report-design-view-report-builder.md)   
 [Vista de diseño de conjunto de datos compartidos &#40;Generador de informes&#41;](../report-builder/shared-dataset-design-view-report-builder.md)   
 [Diseñadores de consultas de Reporting Services](../reporting-services-query-designers.md)  
  
  
