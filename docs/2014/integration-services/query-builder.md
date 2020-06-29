---
title: Generador de consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder dialog box
ms.assetid: 780752c9-6e3c-4f44-aaff-4f4d5e5a45c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 81be066d92ef1e19a141414dad4359b60efca2f9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423162"
---
# <a name="query-builder"></a>Generador de consultas
  Utilice el cuadro de diálogo **Generador de consultas** para crear una consulta para su uso en la tarea Ejecutar SQL, el origen de OLE DB y el destino de OLE DB, y la transformación de búsqueda.  
  
 Puede utilizar el Generador de consultas para realizar las siguientes tareas:  
  
-   **Trabajar con una representación gráfica de una consulta o con comandos SQL** El Generador de comandos tiene un panel en el que se muestra gráficamente la consulta y otro en el que se muestra el texto SQL de la consulta. Puede trabajar en el panel gráfico o en el panel de texto. El Generador de consultas sincroniza las vistas para que siempre estén actualizadas.  
  
-   **Combinar tablas relacionadas** Si agrega más de una tabla a la consulta, el Generador de consultas determinará automáticamente cómo están relacionadas las tablas y generará el comando de combinación correspondiente.  
  
-   **Consultar o actualizar bases de datos** Puede usar el Generador de consultas para devolver datos mediante instrucciones SELECT de Transact-SQL y para crear consultas que actualicen, agreguen o eliminen registros en una base de datos.  
  
-   **Ver y editar resultados inmediatamente** Puede ejecutar la consulta y trabajar con un conjunto de registros en una cuadrícula que le permite desplazarse por los registros de la base de datos y editarlos.  
  
 Las herramientas gráficas del cuadro de diálogo **Generador de consultas** le permiten crear consultas mediante operaciones de arrastrar y colocar. De forma predeterminada, el cuadro de diálogo Generador de consultas construye consultas SELECT, aunque también se pueden crear consultas INSERT, UPDATE o DELETE. Todos los tipos de instrucciones SQL se pueden analizar y ejecutar en el cuadro de diálogo **Generador de consultas** . Para obtener más información sobre la presencia de instrucciones SQL en paquetes, vea [Consultas de Integration Services &#40;SSIS&#41;](integration-services-ssis-queries.md).  
  
 Para obtener más información sobre el lenguaje Transact-SQL y su sintaxis, vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference).  
  
 Asimismo, puede utilizar variables en una consulta para proporcionar valores a un parámetro de entrada, capturar valores de parámetros de salida y almacenar códigos de retorno. Para obtener más información sobre cómo usar variables en las consultas que usan los paquetes, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md), [Origen de OLE DB](data-flow/ole-db-source.md)y [Integration Services &#40;SSIS&#41; Queries](integration-services-ssis-queries.md). Para obtener más información sobre cómo usar variables en la tarea Ejecutar SQL, vea [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) y [Conjuntos de resultados en la tarea Ejecutar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md).  
  
 Las transformaciones de búsqueda Aproximada y Búsqueda también pueden utilizar variables con parámetros y códigos de retorno. Además, la información relativa al origen OLE DB se puede aplicar a estas dos transformaciones.  
  
## <a name="options"></a>Opciones  
 **Barra**  
 Use la barra de herramientas para administrar conjuntos de datos, seleccionar los paneles que desea mostrar y controlar funciones de consulta.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Mostrar u ocultar panel de diagrama**|Muestra u oculta el panel **Diagrama** .|  
|**Mostrar u ocultar panel de cuadrícula**|Muestra u oculta el panel **Cuadrícula** .|  
|**Mostrar u ocultar panel de SQL**|Muestra u oculta el panel **SQL** .|  
|**Mostrar u ocultar panel de resultados**|Muestra u oculta el panel **Resultados** .|  
|**Ejecutar**|Ejecuta la consulta. Los resultados se mostrarán en el panel de resultados.|  
|**Comprobar SQL**|Comprueba que la instrucción SQL sea válida.|  
|**Orden ascendente**|Ordena las filas de salida de la columna seleccionada en el panel de cuadrícula en orden ascendente.|  
|**Orden descendente**|Ordena las filas de salida de la columna seleccionada en el panel de cuadrícula en orden descendente.|  
|**Quitar filtro**|Seleccione un nombre de columna en el panel de cuadrícula y, a continuación, haga clic en **Quitar filtro** para quitar los criterios de ordenación de dicha columna.|  
|**Usar GROUP BY**|Agrega la funcionalidad GROUP BY a la consulta.|  
|**Agregar tabla**|Agrega una nueva tabla a la consulta.|  
  
 **Definición de la consulta**  
 La definición de la consulta proporciona una barra de herramientas y paneles en los que se define y prueba la consulta.  
  
|Panel|Descripción|  
|----------|-----------------|  
|Panel **Diagrama**|Muestra la consulta en un diagrama. El diagrama muestra las tablas incluidas en la consulta y cómo se combinan. Active o desactive la casilla situada junto a una columna de la tabla para agregarla a (o quitarla de) la salida de la consulta.<br /><br /> Cuando agrega tablas a la consulta, el Generador de consultas crea combinaciones entre las tablas basadas en tablas, según las claves de la tabla. Para agregar una combinación, arrastre un campo de una de las tablas a un campo de otra tabla. Para administrar una combinación, haga clic con el botón secundario en la combinación y, a continuación, seleccione una opción de menú.<br /><br /> Haga clic con el botón secundario en el panel **Diagrama** para agregar o quitar tablas, seleccionar todas las tablas y mostrar u ocultar paneles.|  
|Panel **cuadrícula**|Muestra la consulta en una cuadrícula. Puede utilizar este panel para agregar y quitar columnas de una consulta y cambiar la configuración de cada columna.|  
|Panel **SQL**|Muestra la consulta como texto SQL. Los cambios que se realicen en el panel **Diagrama** y en el panel **Cuadrícula** aparecerán aquí, y los cambios que se realicen aquí aparecerán en el panel **Diagrama** y en el panel **Cuadrícula** .|  
|Panel de **resultados**|Muestra los resultados de la consulta al hacer clic en **Ejecutar** en la barra de herramientas.|  
  
## <a name="see-also"></a>Consulte también  
 [Tarea ejecutar SQL](control-flow/execute-sql-task.md)   
 [Origen de OLE DB](data-flow/ole-db-source.md)   
 [Destino de OLE DB](data-flow/ole-db-destination.md)   
 [Transformación búsqueda](data-flow/transformations/lookup-transformation.md)   
 [Integration Services &#40;consultas&#41; SSIS](integration-services-ssis-queries.md)   
 [MERGE en paquetes de Integration Services](control-flow/merge-in-integration-services-packages.md)  
  
  
