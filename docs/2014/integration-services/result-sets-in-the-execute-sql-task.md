---
title: Conjuntos de resultados en la tarea Ejecutar SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
caps.latest.revision: 30
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d1ff4dd56ea104d32a2821bc826ad8919712aea1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217565"
---
# <a name="result-sets-in-the-execute-sql-task"></a>Conjuntos de resultados en la tarea Ejecutar SQL
  En un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , el hecho de que se devuelva un conjunto de resultados a la tarea Ejecutar SQL depende del tipo de comando SQL que use la tarea. Por ejemplo, una instrucción SELECT suele devolver un conjunto de resultados; en cambio, una instrucción INSERT no lo devuelve.  
  
 El contenido del conjunto de resultados también varía en función del comando SQL. Por ejemplo, el conjunto de resultados de una instrucción SELECT puede contener cero filas, una fila o muchas filas. Sin embargo, el conjunto de resultados de una instrucción SELECT que devuelve un recuento o suma contiene exclusivamente una fila.  
  
 Trabajar con conjuntos de resultados en una tarea Ejecutar SQL es algo más que saber si el comando SQL devuelve un conjunto de resultados y cuál es el contenido de este. Existen requisitos de uso e instrucciones adicionales para usar correctamente los conjuntos de resultados en la tarea Ejecutar SQL. El resto de este tema abarca estos requisitos de uso e instrucciones:  
  
-   [Especificar un tipo de conjunto de resultados](#Result_set_type)  
  
-   [Rellenar una variable con un conjunto de resultados](#Populate_variable_with_result_set)  
  
-   [Configurar conjuntos de resultados en el Editor de tareas de ejecución SQL](#Configure_result_sets)  
  
##  <a name="Result_set_type"></a> Especificar un conjunto de resultados tipo  
 La tarea Ejecutar SQL admite los siguientes tipos de conjuntos de resultados:  
  
-   El conjunto de resultados **Ninguno** se usa cuando la consulta no devuelve ningún resultado. Por ejemplo, este conjunto de resultados se utiliza para consultas que agregan, cambian y eliminan registros de una tabla.  
  
-   El conjunto de resultados **Fila única** se usa cuando la consulta devuelve una sola fila. Por ejemplo, este conjunto de resultados se utiliza en una instrucción SELECT que devuelve un recuento o suma.  
  
-   El conjunto de resultados **Conjunto de resultados completo** se usa cuando la consulta devuelve múltiples filas. Por ejemplo, este conjunto de resultados se usa para una instrucción SELECT que recupera todas las filas de una tabla.  
  
-   El conjunto de resultados **XML** se usa cuando la consulta devuelve un conjunto de resultados en formato XML. Por ejemplo, este conjunto de resultados se usa para una instrucción SELECT que incluya una cláusula FOR XML.  
  
 Si la tarea Ejecutar SQL utiliza el conjunto de resultados **Conjunto de resultados completo** y la consulta devuelve varios conjuntos de filas, la tarea solo devuelve el primero de ellos. Si el primer conjunto de filas genera un error, la tarea lo notifica. Si otros conjuntos de filas generan errores, la tarea no los notifica.  
  
##  <a name="Populate_variable_with_result_set"></a> Llenar una Variable con un conjunto de resultados  
 Puede enlazar el conjunto de resultados devuelto por una consulta con una variable definida por el usuario si el tipo del conjunto de resultados es una fila individual, un conjunto de filas o XML.  
  
 Si el tipo de conjunto de resultados es **Fila única**, puede enlazar una columna del resultado devuelto a una variable utilizando el nombre de la columna como nombre del conjunto de resultados, o puede utilizar la posición ordinal de la columna en la lista de columnas como dicho nombre. Por ejemplo, el nombre del conjunto de resultados para la consulta `SELECT Color FROM Production.Product WHERE ProductID = ?` puede ser **Color** o **0**. Si la consulta devuelve varias columnas y desea obtener acceso a los valores de todas ellas, debe enlazar cada columna a una variable distinta. Si asigna columnas a variables utilizando números como nombre de los conjuntos de resultados, los números reflejan el orden de aparición de las columnas en la lista de columnas de la consulta. Por ejemplo, en la consulta `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`, puede utilizar 0 para la columna **Color** y 1 para la columna **ListPrice** . La capacidad de utilizar un nombre de columna como nombre del conjunto de resultados dependerá del proveedor para el que se haya configurado la tarea. No todos los proveedores ponen los nombres de columna a disposición.  
  
 Es posible que algunas consultas que devuelven un valor único no incluyan nombres de columnas. Por ejemplo, la instrucción `SELECT COUNT (*) FROM Production.Product` no devuelve un nombre de columna. Puede tener acceso al resultado devuelto utilizando la posición ordinal 0 como nombre del resultado. Para tener acceso al resultado devuelto por nombre de columna, la consulta debe incluir una cláusula AS \<nombre de alias> para proporcionar un nombre de columna. La instrucción `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`proporciona la columna **CountOfProduct** . Luego puede tener acceso al resultado devuelto utilizando el nombre de la columna **CountOfProduct** o la posición ordinal 0.  
  
 Si el tipo de conjunto de resultados es **Conjunto de resultados completo** o **XML**, debe utilizar 0 como nombre del conjunto de resultados.  
  
 Cuando se asigna una variable a un conjunto de resultados con el tipo de conjunto de resultados **Fila única** , la variable debe tener un tipo de datos que sea compatible con el tipo de datos de la columna contenida en el conjunto de resultados. Por ejemplo, un conjunto de resultados que contiene una columna con un tipo de datos `String` no se puede asignar a una variable con un tipo de datos numérico. Al establecer el **TypeConversionMode** propiedad `Allowed`, la tarea Ejecutar SQL intentará convertir el parámetro de salida y resultados a los datos de tipo de la variable de los resultados de consulta que se asignan.  
  
 Un conjunto de resultados XML solamente se puede asignar a una variable con el tipo de datos `String` o `Object`. Si la variable tiene el `String` tipo de datos, la tarea Ejecutar SQL devuelve una cadena y el origen XML pueden consumir los datos XML. Si la variable tiene el `Object` tipo de datos, la tarea Ejecutar SQL devuelve un objeto de Document Object Model (DOM).  
  
 Un **conjunto de resultados completo** debe asignar a una variable de la `Object` tipo de datos. El resultado devuelto es un objeto de conjunto de filas. Puede usar un contenedor de bucle Foreach para extraer los valores de las filas de una tabla almacenados en la variable Object y almacenarlos en las variables de paquete y, entonces, utilizar una tarea Script para escribir los datos almacenados en variables de paquetes en un archivo. Para ver una demostración de cómo usar un contenedor de bucle Foreach y una tarea Script, consulte el ejemplo en CodePlex, [Ejecutar parámetros SQL y conjuntos de resultados](http://go.microsoft.com/fwlink/?LinkId=157863), en msftisprodsamples.codeplex.com.  
  
 En la tabla siguiente se resumen los tipos de datos de variables que se pueden asignar a conjuntos de resultados.  
  
|Tipo de conjunto de resultados|Tipo de datos de variable|Tipo de objeto|  
|---------------------|---------------------------|--------------------|  
|Fila única|Cualquier tipo que sea compatible con la columna de tipo del conjunto de resultados.|No aplicable|  
|Conjunto de resultados completo|`Object`|Si la tarea utiliza un administrador de conexiones nativo, incluidos los administradores de conexión ADO, OLE DB, Excel y ODBC, el objeto devuelto es ADO `Recordset`.<br /><br /> Si la tarea usa un administrador de conexiones administrado, como el [!INCLUDE[vstecado](../includes/vstecado-md.md)] Administrador de conexiones, el objeto devuelto es un `System.Data.DataSet`.<br /><br /> Puede usar una tarea Script para tener acceso a la `System.Data.DataSet` de objeto, como se muestra en el ejemplo siguiente.<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|Si la tarea utiliza un administrador de conexiones nativo, incluidos los administradores de conexión ADO, OLE DB, Excel y ODBC, el objeto devuelto es un `MSXML6.IXMLDOMDocument`.<br /><br /> Si la tarea usa un administrador de conexiones administrado, como el administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)], el objeto devuelto es un `System.Xml.XmlDocument`.|  
  
 La variable puede definirse en el ámbito de la tarea Ejecutar SQL o en el ámbito del paquete. Si la variable tiene ámbito de paquete, el conjunto de resultados estará disponible para otras tareas y otros contenedores del paquete, así como para cualquier paquete ejecutado por la tarea Ejecutar paquete o Ejecutar paquete DTS 2000.  
  
 Cuando se asigna una variable a un conjunto de resultados de **fila única** , los valores que no son de cadena devueltos por la instrucción SQL se convierten en cadenas cuando se cumplen las condiciones siguientes:  
  
-   La propiedad **TypeConversionMode** se establece en True. Establezca el valor de propiedad en la ventana Propiedades o mediante el **Editor de la tarea Ejecutar SQL**.  
  
-   La conversión no producirá el truncamiento de datos.  
  
 Para obtener información sobre cómo cargar un conjunto de resultados en una variable, vea [Asignar conjuntos de resultados a variables en una tarea Ejecutar SQL](control-flow/execute-sql-task.md).  
  
##  <a name="Configure_result_sets"></a> Configurar conjuntos de resultados la tarea Ejecutar SQL  
 Para obtener más información acerca de las propiedades de los conjuntos de resultados que puede establecer en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Ejecutar el Editor de la tarea SQL &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Asignar conjuntos de resultados a variables en una tarea Ejecutar SQL](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Ejemplo CodePlex, [Ejecutar conjuntos de resultados y parámetros de SQL](http://go.microsoft.com/fwlink/?LinkId=157863)(en inglés), en msftisprodsamples.codeplex.com  
  
  
