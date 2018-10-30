---
title: Diseñador de consultas de lista de SharePoint (Generador de informes) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
f1_keywords:
- "10016"
ms.assetid: b8a3122c-8008-4950-b515-937636d7967f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 701cccc9acc67c21133d97b592f7aa6211adb8d4
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031624"
---
# <a name="sharepoint-list-query-designer-report-builder"></a>Diseñador de consultas de lista de SharePoint (Generador de informes)
  El Generador de informes y el Diseñador de informes proporcionan un diseñador gráfico de consultas y un diseñador de consultas basados en texto para ayudarle a crear una consulta que especifique los datos que deben recuperarse de un sitio de SharePoint para un conjunto de datos de informe. Use el diseñador gráfico de consultas para explorar los metadatos de la lista de SherPoint, crear una consulta de forma interactiva y ver los resultados de la consulta. Use el diseñador de consultas basado en texto para ver la consulta creada por el diseñador gráfico de consultas, modificar una consulta o escribir los comandos de la consulta. También puede importar una consulta existente de un archivo o informe.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
## <a name="graphical-query-designer"></a>Diseñador gráfico de consultas  
 En el diseñador gráfico de consultas puede el explorador el sitio de SharePoint, compilar interactivamente el comando que recupera los datos de la lista de SharePoint para un conjunto de datos. Debe elegir los campos que se incluirán en el conjunto de datos y, si lo desea, especificar los filtros que limitan los datos en el conjunto de datos. Puede especificar que los filtros se usan como parámetros y proporcionar el valor del filtro en tiempo de ejecución.  
  
 Las listas de SharePoint incluyen un gran número de campos concretos de SharePoint que podría no ser útil incluir en los informes. El diseñador de consultas proporciona una opción para ocultar estos campos y facilitar y agilizar la determinación de los campos que se utilizan.  
  
 El diseñador gráfico de consultas se divide en tres áreas.  
  
-   Panel de exploración en el que se seleccionan los elementos de lista y los campos que se utilizan.  
  
-   El área de diseño en la que se genera la consulta.  
  
-   El panel de resultados en el que se ven los resultados de la consulta.  
  
 La figura siguiente muestra el diseñador gráfico de consultas cuando se utiliza con listas de SharePoint.  
  
 ![rsQD_Relational_Graphical_SharePoint](../../reporting-services/report-data/media/rsqd-relational-graphical-sharepoint.gif "rsQD_Relational_Graphical_SharePoint")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
 [Listas de SharePoint](#DatabaseView)  
 Muestra las listas de SharePoint y los campos dentro de cada elemento de la lista.  
  
 [Campos seleccionados](#SelectedFields)  
 Muestra la lista de nombres de campo de SharePoint de los elementos seleccionados en el panel Listas de SharePoint. Estos campos se convierten en la colección de campos para el conjunto de datos de informe.  
  
 [Filtros aplicados.](#AppliedFilters)  
 Muestra una lista de campos y criterios de filtro para tablas o vistas en la Vista de base de datos.  
  
 [Resultados de la consulta](#QueryResults)  
 Muestra datos de ejemplo para el conjunto de resultados de la consulta generada automáticamente.  
  
###  <a name="DatabaseView"></a> Panel Listas de SharePoint  
 El panel Listas de SharePoint muestra los metadatos de los objetos de base de datos que el usuario tiene permiso para ver, que se determinan mediante la conexión a un origen de datos y las credenciales. La vista jerárquica muestra objetos de base de datos organizados por esquema de la base de datos. Expanda el nodo de cada esquema para ver las tablas, vistas, procedimientos almacenados y funciones con valores de tabla. Expanda una tabla o vista para ver las columnas.  
  
###  <a name="SelectedFields"></a> Panel Campos seleccionados  
 El panel Campos seleccionados muestra los campos de elemento de lista que selecciona para los elementos de lista de SharePoint. Los campos que se muestran en este panel se convierten en la colección de campos para el conjunto de datos de informe. Una vez creado el conjunto de datos y una consulta, use el panel Datos de informe para ver la colección de campos para un conjunto de datos de informe. Estos campos representan los datos que pueden mostrarse en tablas, gráficos y otros elementos de informe al visualizar un informe.  
  
 Para agregar o quitar campos en este panel, active o desactive las casillas de los campos de tabla o vista en el panel Listas de SharePoint.  
  
###  <a name="AppliedFilters"></a> Panel Filtros aplicados  
 El panel Filtros aplicados muestra los criterios que se usan para limitar el número de filas de datos que deben recuperarse en tiempo de ejecución. Los criterios especificados en este panel se usan para generar una cláusula WHERE de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Al seleccionar la opción de parámetro, se crea automáticamente un parámetro de informe. Los parámetros de informe basados en los parámetros de consulta permiten a un usuario especificar valores para que la consulta controle los datos del informe.  
  
 Se muestran las siguientes columnas:  
  
-   **Nombre de campo** : muestra el nombre del campo al que deben aplicarse los criterios.  
  
-   **Operador** : muestra la operación que debe usarse en la expresión de filtro.  
  
-   **Valor** : muestra el valor que debe usarse en la expresión de filtro.  
  
-   **Parámetro** : muestra la opción de agregar un parámetro de consulta a la consulta. Use las propiedades del conjunto de datos para ver la relación que existe entre el parámetro de consulta y el parámetro de informe.  
  
###  <a name="QueryResults"></a> Panel Resultados de la consulta  
 El panel Resultados de la consulta muestra los resultados de la consulta generada automáticamente que se especifica mediante selecciones en los otros paneles. Las columnas del conjunto de resultados son los campos que se especifican en el panel Campos seleccionados y los datos de fila quedan limitados por los filtros especificados en el panel Filtros aplicados.  
  
 Estos datos representan los valores del origen de datos en el momento de ejecución de la consulta. Los datos no se guardan en la definición de informe. Los datos reales del informe se recuperar al procesar el informe.  
  
 El criterio de ordenación del conjunto de resultados se determina según el orden de los datos recuperados del origen de datos. El criterio de ordenación puede cambiarse modificando la consulta o después de recuperar los datos para el informe.  
  
### <a name="graphical-query-designer-toolbar"></a>Barra de herramientas del diseñador gráfico de consultas  
 La barra de herramientas del diseñador de consultas relacionales ofrece los siguientes botones para ayudarle a especificar o ver los resultados de una consulta.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Cambie al diseñador de consultas basado en texto para ver la consulta generada automáticamente o para modificar la consulta.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivo .sql y .rdl.|  
|**Ejecutar consulta**|Ejecuta la consulta. El panel Resultados de la consulta muestra el conjunto de resultados.|  
|**Mostrar campos ocultos**|Alterna entre mostrar u ocultar los campos que SharePoint generó automáticamente como el ProgID y Level para los elementos de vínculo de SharePoint, pero normalmente no se utiliza en informes. Al ocultar estos campos, la lista de campos se hace más corta y más fácil de utilizar.|  
  
## <a name="see-also"></a>Ver también  
 [Diseñadores de consultas &#40;Generador de informes&#41;](https://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
