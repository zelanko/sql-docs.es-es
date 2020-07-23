---
title: Consultas de Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 01a292229c29720b91d66d1f607b375b759e75fe
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917501"
---
# <a name="integration-services-ssis-queries"></a>Consultas de Integration Services (SSIS)

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  La tarea Ejecutar SQL, el origen de OLE DB, el destino de OLE DB y la transformación Búsqueda pueden utilizar consultas de SQL. En la tarea Ejecutar SQL, las instrucciones SQL pueden crear, actualizar y eliminar datos y objetos de bases de datos, ejecutar procedimientos almacenados y ejecutar instrucciones SELECT. En el origen de OLE DB y la transformación Búsqueda, las instrucciones SQL son normalmente instrucciones SELECT o EXEC. Normalmente, éstas últimas ejecutan procedimientos almacenados que devuelven conjuntos de resultados.  
  
 Una consulta se puede analizar para ver si es válida. Al analizar una consulta que usa una conexión a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la consulta se analiza, se ejecuta y el resultado de la ejecución (correcta o errónea) se asigna al resultado del análisis. Si la consulta utiliza una conexión a datos que no sean de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la instrucción solo se analiza.  
  
Puede proporcionar la instrucción SQL de las maneras siguientes:
1.   Escríbala directamente en el diseñador.
2.   Especifique una conexión a un archivo que contenga la instrucción.
3.   Especifique una variable que contenga la instrucción.  
  
## <a name="direct-input-sql"></a>Entrada directa en SQL  
 El Generador de consultas está disponible en la interfaz de usuario de la tarea Ejecutar SQL, el origen de OLE DB, el destino de OLE DB y la transformación Búsqueda. El Generador de consultas ofrece las siguientes ventajas:  
  
-   Trabajar visualmente o con comandos SQL.  
  
     El Generador de consultas incluye paneles gráficos que muestran la consulta visualmente y un panel de texto que muestra el texto SQL de la consulta. Puede trabajar en los paneles gráficos o de texto. El Generador de consultas sincroniza las vistas de forma que el texto de la consulta y la representación gráfica de la consulta coincidan siempre.  
  
-   Combinar tablas relacionadas.  
  
     Si agrega más de una tabla a la consulta, el Generador de consultas determinará automáticamente cómo están relacionadas las tablas y generará el comando de combinación correspondiente.  
  
-   Consultar o actualizar bases de datos.  
  
     Puede utilizar el Generador de consultas para devolver datos mediante instrucciones SELECT de Transact-SQL, o bien para crear consultas que actualicen, agreguen o eliminen registros de una base de datos.  
  
-   Ver y modificar los resultados inmediatamente.  
  
     Puede ejecutar la consulta y trabajar con un conjunto de registros en una cuadrícula que le permita desplazarse por los registros de la base de datos y modificarlos.  
  
 A pesar de que el Generador de consultas tiene limitaciones visuales para crear consultas SELECT, puede escribir el SQL para otros tipos de instrucciones, como las instrucciones DELETE y UPDATE, en el panel de texto. El panel gráfico se actualiza automáticamente para reflejar la instrucción SQL que escribió.  
  
 También puede proporcionar entradas directas escribiendo la consulta en el cuadro de diálogo de la tarea o del componente de flujo de datos, o bien en la ventana Propiedades.  
  
 Para más información, consulte [Query Builder](https://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5).  
  
## <a name="sql-in-files"></a>SQL en archivos  
 La instrucción SQL para la tarea Ejecutar SQL también puede residir en un archivo independiente. Por ejemplo, puede escribir una consulta utilizando herramientas como el Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], guardarla en un archivo y después, leer la consulta del archivo al ejecutar un paquete. El archivo solo puede contener las instrucciones SQL que se van a ejecutar y comentarios. Para utilizar una instrucción SQL almacenada en un archivo, debe proporcionar una conexión de archivos que especifique el nombre y la ubicación del archivo. Para obtener más información, consulte [File Connection Manager](../integration-services/connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL en variables  
 Si el origen de la instrucción SQL en la tarea Ejecutar SQL es una variable, debe proporcionar el nombre de la variable que contiene la consulta. La propiedad Value de la variable contiene el texto de la consulta. La propiedad ValueType de la variable se establece en un tipo de datos de cadena y luego se escribe o se copia la instrucción SQL en la propiedad Value. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md) y [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  

## <a name="query-builder-dialog-box"></a>Generador de consultas, cuadro de diálogo
Utilice el cuadro de diálogo **Generador de consultas** para crear una consulta para su uso en la tarea Ejecutar SQL, el origen de OLE DB y el destino de OLE DB, y la transformación de búsqueda.  
  
 Puede utilizar el Generador de consultas para realizar las siguientes tareas:  
  
-   **Trabajar con una representación gráfica de una consulta o con comandos SQL** El Generador de comandos tiene un panel en el que se muestra gráficamente la consulta y otro en el que se muestra el texto SQL de la consulta. Puede trabajar en el panel gráfico o en el panel de texto. El Generador de consultas sincroniza las vistas para que siempre estén actualizadas.  
  
-   **Combinar tablas relacionadas** Si agrega más de una tabla a la consulta, el Generador de consultas determinará automáticamente cómo están relacionadas las tablas y generará el comando de combinación correspondiente.  
  
-   **Consultar o actualizar bases de datos** Puede usar el Generador de consultas para devolver datos mediante instrucciones SELECT de Transact-SQL y para crear consultas que actualicen, agreguen o eliminen registros en una base de datos.  
  
-   **Ver y editar resultados inmediatamente** Puede ejecutar la consulta y trabajar con un conjunto de registros en una cuadrícula que le permite desplazarse por los registros de la base de datos y editarlos.  
  
 Las herramientas gráficas del cuadro de diálogo **Generador de consultas** le permiten crear consultas mediante operaciones de arrastrar y colocar. De forma predeterminada, el cuadro de diálogo Generador de consultas construye consultas SELECT, aunque también se pueden crear consultas INSERT, UPDATE o DELETE. Todos los tipos de instrucciones SQL se pueden analizar y ejecutar en el cuadro de diálogo **Generador de consultas** . Para obtener más información sobre la presencia de instrucciones SQL en paquetes, vea [Consultas de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-queries.md).  
  
 Para obtener más información sobre el lenguaje Transact-SQL y su sintaxis, vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](../t-sql/transact-sql-reference-database-engine.md).  
  
 Asimismo, puede utilizar variables en una consulta para proporcionar valores a un parámetro de entrada, capturar valores de parámetros de salida y almacenar códigos de retorno. Para obtener más información sobre cómo usar variables en las consultas que usan los paquetes, vea [Tarea Ejecutar SQL](../integration-services/control-flow/execute-sql-task.md), [Origen de OLE DB](../integration-services/data-flow/ole-db-source.md)y [Integration Services &#40;SSIS&#41; Queries](../integration-services/integration-services-ssis-queries.md). Para obtener más información sobre cómo usar variables en la tarea Ejecutar SQL, vea [Parámetros y códigos de retorno en la tarea Ejecutar SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663) y [Conjuntos de resultados en la tarea Ejecutar SQL](https://msdn.microsoft.com/library/62605b63-d43b-49e8-a863-e154011e6109).  
  
 Las transformaciones de búsqueda Aproximada y Búsqueda también pueden utilizar variables con parámetros y códigos de retorno. Además, la información relativa al origen OLE DB se puede aplicar a estas dos transformaciones.  
  
### <a name="options"></a>Opciones  
 **Barra de herramientas**  
 Use la barra de herramientas para administrar conjuntos de datos, seleccionar los paneles que desea mostrar y controlar funciones de consulta.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Mostrar u ocultar panel de diagrama**|Muestra u oculta el panel **Diagrama** .|  
|**Mostrar u ocultar panel de cuadrícula**|Muestra u oculta el panel **Cuadrícula** .|  
|**Mostrar u ocultar panel de SQL**|Muestra u oculta el panel de **SQL** .|  
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
|Panel**Diagrama**|Muestra la consulta en un diagrama. El diagrama muestra las tablas incluidas en la consulta y cómo se combinan. Active o desactive la casilla situada junto a una columna de la tabla para agregarla a (o quitarla de) la salida de la consulta.<br /><br /> Cuando agrega tablas a la consulta, el Generador de consultas crea combinaciones entre las tablas basadas en tablas, según las claves de la tabla. Para agregar una combinación, arrastre un campo de una de las tablas a un campo de otra tabla. Para administrar una combinación, haga clic con el botón secundario en la combinación y, a continuación, seleccione una opción de menú.<br /><br /> Haga clic con el botón derecho en el panel **Diagrama** para agregar o quitar tablas, seleccionar todas las tablas y mostrar u ocultar paneles.|  
|Panel**Cuadrícula**|Muestra la consulta en una cuadrícula. Puede utilizar este panel para agregar y quitar columnas de una consulta y cambiar la configuración de cada columna.|  
|Panel**SQL**|Muestra la consulta como texto SQL. Los cambios que se realicen en el panel **Diagrama** y en el panel **Cuadrícula** aparecerán aquí, y los cambios que se realicen aquí aparecerán en el panel **Diagrama** y en el panel **Cuadrícula** .|  
|Panel**Resultados**|Muestra los resultados de la consulta al hacer clic en **Ejecutar** en la barra de herramientas.| 

  
