---
title: Interfaz de usuario del Diseñador de consultas basado en texto (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
helpviewer_keywords:
- query designers, text-based
ms.assetid: 89fddca5-bd96-4128-9072-5348d1b6e02c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d2eecd40de68a6678b3011d15fc13f7cf9757022
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111875"
---
# <a name="text-based-query-designer-user-interface-report-builder"></a>Interfaz de usuario del Diseñador de consultas basado en texto (Generador de informes)
  Use el diseñador de consultas basado en texto para especificar una consulta mediante el lenguaje de consulta admitido por el origen de datos, para ejecutar la consulta y para ver los resultados en tiempo de diseño. Puede especificar varias sintaxis de consulta, comandos o instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] para extensiones de procesamiento de datos personalizadas, y consultas que se especifican como expresiones. Dado que el generador de consultas basado en texto no procesa previamente la consulta y puede acomodar todo tipo de sintaxis de consulta, es la herramienta de generación de consultas predeterminada para varios tipos de orígenes de datos.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
 El diseñador de consultas basado en texto muestra una barra de herramientas y los dos paneles siguientes:  
  
-   **Consulta** Muestra el texto de la consulta, el nombre de tabla o el nombre del procedimiento almacenado, dependiendo del tipo de consulta. No todos los tipos de consulta están disponibles para todos los tipos de origen de datos. Por ejemplo, el nombre de tabla solamente es compatible con el tipo de orígenes de datos OLE DB.  
  
-   **Resultado** Muestra los resultados de la ejecución de la consulta en tiempo de diseño.  
  
## <a name="text-based-query-designer-toolbar"></a>Barra de herramientas del diseñador de consultas basado en texto  
 El diseñador de consultas basado en texto proporciona una sola barra de herramientas para todos los tipos de comando. La tabla siguiente contiene una lista con los botones de la barra de herramientas y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas. No todos los tipos de orígenes de datos admiten diseñadores gráficos de consultas.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivo sql y rdl.|  
|![Ejecutar la consulta](../../analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra el conjunto de resultados en el panel Resultado.|  
|**Tipo de comando**|Seleccione **Text**, **StoredProcedure**o **TableDirect**. Si un procedimiento almacenado tiene parámetros, el cuadro de diálogo **Definir parámetros de consulta** aparece al hacer clic en **Ejecutar** en la barra de herramientas; puede rellenar los valores según sea necesario.<br /><br /> Nota: Si un procedimiento almacenado devuelve más de un conjunto de resultados, solo se usa el primero para rellenar el conjunto de datos.|  
  
### <a name="command-type-text"></a>Tipo de comando Text  
 Al crear un conjunto de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el diseñador de consultas relacionales se abre de forma predeterminada. Para cambiar al diseñador de consultas basado en texto, haga clic en el botón de alternancia **Editar como texto** de la barra de herramientas. El diseñador de consultas basado en texto consta de dos paneles: el panel Consulta y el panel Resultado. En la siguiente ilustración se indica el nombre de cada panel.  
  
 ![Diseñador de consultas genérico, para consultas de datos relacionales](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "Diseñador de consultas genérico, para consultas de datos relacionales")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Consulta|Muestra el texto de consulta de [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Use este panel para escribir o editar una consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] .|  
|Resultado|Muestra los resultados de la consulta. Para ejecutar la consulta, haga clic con el botón derecho en cualquier panel y haga clic en **Ejecutar**, o bien haga clic en el botón **Ejecutar** de la barra de herramientas.|  
  
#### <a name="example"></a>Ejemplo  
 La consulta siguiente devuelve la lista de apellidos de la [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008** base de datos `ContactType` de tabla para el `Person` esquema.  
  
```  
SELECT Name FROM Person.ContactType  
```  
  
 Si hace clic en **Ejecutar** en la barra de herramientas, el comando del panel **Consulta** se ejecuta y los resultados se muestran en el panel **Resultado** . El conjunto de resultados muestra una lista de 20 tipos de contactos; por ejemplo, Owner o Sales Agent.  
  
### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure  
 Si selecciona **Tipo de comando StoredProcedure**, el diseñador de consultas basado en texto presenta dos paneles: el panel Consulta y el panel Resultado. Escriba el nombre del procedimiento almacenado en el panel Consulta y haga clic en **Ejecutar** en la barra de herramientas. Si el procedimiento almacenado utiliza parámetros, se abre el cuadro de diálogo **Definir parámetros de consulta** . Escriba los valores de los parámetros para el procedimiento almacenado. Se crea un parámetro de informe para cada parámetro de entrada de procedimiento almacenado.  
  
 La figura siguiente muestra los paneles Consulta y Resultado al ejecutar un procedimiento almacenado. En este caso, los parámetros de entrada son constantes.  
  
 ![Procedimiento almacenado en un diseñador de consultas basado en texto](../../analysis-services/media/rs-relational-text-sp.gif "Procedimiento almacenado en un diseñador de consultas basado en texto")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Consulta|Muestra el nombre del procedimiento almacenado y de los parámetros de entrada.|  
|Resultado|Muestra los resultados de la consulta. Para ejecutar la consulta, haga clic con el botón derecho en cualquier panel y haga clic en **Ejecutar**, o bien haga clic en el botón **Ejecutar** de la barra de herramientas.|  
  
#### <a name="example"></a>Ejemplo  
 La siguiente consulta llama a la [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008** procedimiento almacenado `uspGetWhereUsedProductID`. Debe especificar un valor para el parámetro de número de identificación de producto al ejecutar la consulta.  
  
```  
uspGetWhereUsedProductID  
```  
  
 Haga clic en el botón **Ejecutar** (**!**). Cuando se le soliciten los parámetros de consulta, use la tabla siguiente para escribir los valores.  
  
|||  
|-|-|  
|*@StartProductID*|820|  
|*@CheckDate*|20010115|  
  
 Para la fecha especificada, el conjunto de resultados muestra una lista de 13 identificadores del producto que utilizaron el número de componente especificado.  
  
### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect  
 Si selecciona **Tipo de comando TableDirect**, el diseñador de consultas basado en texto presenta dos paneles: el panel Consulta y el panel Resultado. Si selecciona una tabla y hace clic en el botón **Ejecutar** , se devolverán todas las columnas de dicha tabla.  
  
#### <a name="example"></a>Ejemplo  
 Para un tipo de origen de datos OLE DB, la siguiente consulta de conjunto de datos devuelve un conjunto de resultados para todos los tipos en el [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008** base de datos.  
  
 `Person.ContactType`  
  
 Especificar el nombre de tabla Person.ContactType equivale a crear la instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] `SELECT * FROM Person.ContactType`.  
  
## <a name="see-also"></a>Vea también  
 [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](relational-query-designer-user-interface-report-builder.md)   
 [Diseñadores de consultas &#40;Generador de informes&#41;](../query-designers-report-builder.md)  
  
  
