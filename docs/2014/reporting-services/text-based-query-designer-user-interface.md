---
title: Interfaz de usuario del diseñador de consultas basado en texto | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd3dfdb640c0e2c1b225b0b3a54fcc8bc3ebabc5
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177255"
---
# <a name="text-based-query-designer-user-interface"></a>Interfaz de usuario del Diseñador de consultas basado en texto
  Use el diseñador de consultas basado en texto para especificar una consulta mediante el lenguaje de consulta admitido por el origen de datos, para ejecutar la consulta y para ver los resultados en tiempo de diseño. Puede especificar varias sintaxis de consulta, comandos o instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] para extensiones de procesamiento de datos personalizadas, y consultas que se especifican como expresiones. Dado que el generador de consultas basado en texto no procesa previamente la consulta y puede acomodar todo tipo de sintaxis de consulta, es la herramienta de generación de consultas predeterminada para varios tipos de orígenes de datos.

 El diseñador de consultas basado en texto muestra una barra de herramientas y los dos paneles siguientes:

-   **Consulta** de Muestra el texto de la consulta, el nombre de la tabla o el nombre del procedimiento almacenado.

-   **Resultado** de Muestra los resultados de la ejecución de la consulta en tiempo de diseño.

## <a name="text-based-query-designer-toolbar"></a>Barra de herramientas del diseñador de consultas basado en texto
 El diseñador de consultas basado en texto proporciona una sola barra de herramientas para todos los tipos de comando. La tabla siguiente contiene una lista con los botones de la barra de herramientas y sus funciones.

|Botón|Descripción|
|------------|-----------------|
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas. No todos los tipos de orígenes de datos admiten diseñadores gráficos de consultas.|
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivos sql y rdl. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|
|![Ejecutar la consulta](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra el conjunto de resultados en el panel Resultado.|
|**Tipo de comando**|Seleccione **Text**, **StoredProcedure**o **TableDirect**. Si un procedimiento almacenado tiene parámetros, el cuadro de diálogo **Definir parámetros de consulta** aparece al hacer clic en **Ejecutar** en la barra de herramientas; puede rellenar los valores según sea necesario. Tenga en cuenta que si un procedimiento almacenado devuelve más de un conjunto de resultados, solo se usa el primer conjunto de resultados para rellenar el conjunto de resultados.<br /><br /> La compatibilidad del tipo de comando varía en función del tipo de origen de datos. Por ejemplo, solamente OLE DB y ODBC son compatibles con **TableDirect**.|

### <a name="command-type-text"></a>Tipo de comando Text
 Cuando se crea un conjunto de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el Diseñador de informes muestra el diseñador gráfico de consultas de forma predeterminada. Para cambiar al diseñador de consultas basado en texto, haga clic en el botón de alternancia **Editar como texto** de la barra de herramientas. El diseñador de consultas basado en texto consta de dos paneles: el panel Consulta y el panel Resultado. En la siguiente ilustración se indica el nombre de cada panel.

 ![Diseñador de consultas genérico, para consultas de datos relacionales](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsaw-sql-generic.gif "Diseñador de consultas genérico, para consultas de datos relacionales")

 En la siguiente tabla se describe la función de cada panel.

|Panel|Función|
|----------|--------------|
|Consultar|Muestra el texto de consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] . Use este panel para escribir o editar una consulta [!INCLUDE[tsql](../includes/tsql-md.md)] .|
|Resultado|Muestra los resultados de la consulta. Para ejecutar la consulta, haga clic con el botón derecho en cualquier panel y haga clic en **Ejecutar**, o bien haga clic en el botón **Ejecutar** de la barra de herramientas.|

#### <a name="example"></a>Ejemplo
 La siguiente consulta devuelve la lista de apellidos de la tabla [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] de la base de datos `Contact`.

```
SELECT LastName FROM Person.Person;
```

 Puede usar cualquier instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] para el tipo de comando Text, incluyendo instrucciones `EXEC`. La siguiente consulta llama al [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] procedimiento `uspGetEmployeeManagers` almacenado y devuelve la cadena de comandos para el empleado con el número de identificación 1.

```
EXEC uspGetEmployeeManagers 1;
```

 Si hace clic en **Ejecutar** en la barra de herramientas, el comando del panel **Consulta** se ejecuta y los resultados se muestran en el panel **Resultado** .

### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure
 Si selecciona **Tipo de comando StoredProcedure**, el diseñador de consultas basado en texto presenta dos paneles: el panel Consulta y el panel Resultado. Escriba el nombre del procedimiento almacenado en el panel Consulta y haga clic en **Ejecutar** en la barra de herramientas. Se abrirá el cuadro de diálogo Definir parámetros de consulta. Escriba los valores de los parámetros para el procedimiento almacenado. Se crea un parámetro de informe para cada parámetro de procedimiento almacenado.

#### <a name="example"></a>Ejemplo
 La consulta siguiente llama al procedimiento almacenado [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] de `uspGetEmployeeManagers`. Debe especificar un valor para el parámetro de número de identificación de empleado al ejecutar la consulta.

```
uspGetEmployeeManagers;
```

### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect
 Si selecciona **Tipo de comando TableDirect**, el diseñador de consultas basado en texto presenta dos paneles: el panel Consulta y el panel Resultado. Si selecciona una tabla y hace clic en el botón **Ejecutar** , se devolverán todas las columnas de dicha tabla.

#### <a name="example"></a>Ejemplo
 La siguiente consulta devuelve un conjunto de resultados para todos los clientes de la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].

 `Sales.Customer`

 Al escribir el nombre de la tabla sales. Customer, es equivalente a crear la [!INCLUDE[tsql](../includes/tsql-md.md)] instrucción. `SELECT * FROM Sales.Customer;`

## <a name="see-also"></a>Consulte también
 [Herramientas de diseño de consultas en Diseñador de informes SQL Server Data Tools &#40;ssrs&#41;](report-data/query-design-tools-ssrs.md) los conjuntos [de archivos incrustados del informe y los conjuntos de valores compartidos &#40;Generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) SQL Server [tipo de conexión &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md) OLE DB [tipo de conexión &#40;SSRS&#41;](report-data/ole-db-connection-type-ssrs.md) [tipo de conexión ODBC &#40;SSRS&#41;](report-data/odbc-connection-type-ssrs.md) los conjuntos [de archivos incrustados del informe y los conjuntos de valores compartidos &#40;generador de informes y SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) [archivo de configuración RSReportDesigner](report-server/rsreportdesigner-configuration-file.md)


