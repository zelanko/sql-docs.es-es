---
title: Tipo de conexión de SQL Server (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 957e7091-e08f-48d2-9506-872227ae8b20
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5d523fe31c6b07ebe835d7353af298c93fd9e90f
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "40410093"
---
# <a name="sql-server-connection-type-ssrs"></a>Tipo de conexión de SQL Server (SSRS)
  Para incluir en el informe los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe tener un conjunto de datos basado en un origen de datos de informe de tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este tipo de origen de datos integrado se basa en la extensión de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use este tipo de origen de datos para conectar y recuperar los datos de la versión actual y de las versiones anteriores de bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Esta extensión de datos admite parámetros de varios valores, agregados del servidor y credenciales administrados con independencia de la cadena de conexión.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Al conectar a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , está conectando con el objeto de base de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor. La base de datos podría tener varios esquemas que tienen varias tablas, vistas y procedimientos almacenados. Especifique el objeto de base de datos que se va a usar en el diseñador de consultas. Si no especifica una base de datos en la cadena de conexión, puede conectar con la base de datos predeterminada que le asignó el administrador de bases de datos.  
  
 Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. El siguiente ejemplo de cadena de conexión especifica una base de datos de ejemplo en el cliente local:  
  
```  
Data Source=<server>;Initial Catalog=AdventureWorks  
```  
  
 Para obtener más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Desde un cliente de creación de informes, están disponibles las siguientes opciones para especificar las credenciales:  
  
-   Usuario actual de Windows (lo que se conoce también como seguridad integrada).  
  
-   Utilizar un nombre de usuario y una contraseña almacenados.  
  
-   Pedir las credenciales al usuario. Esta opción solo admite la seguridad integrada de Windows.  
  
-   No se necesitan credenciales. Para usar esta opción, debe tener la cuenta de ejecución desatendida configurada en el servidor de informes. Para más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en la [documentación de Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) en msdn.microsoft.com.  
  
 Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) o [Especificar credenciales en el Generador de informes](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Consultas  
 Una consulta especifica qué datos se van a recuperar para un conjunto de datos de informe. Las columnas del conjunto de resultados de una consulta rellenan la colección de campos de un conjunto de datos. Un informe procesa solamente el primer conjunto de resultados que recupera una consulta.  
  
 De forma predeterminada, si crea una nueva consulta o abre una consulta existente que puede ser representada en el diseñador gráfico de consultas, este último está disponible. Puede especificar una consulta de varias maneras:  
  
-   Generar una consulta interactivamente. Utilice el diseñador de consultas relacionales que muestra una vista jerárquica de las tablas, las vistas, los procedimientos almacenados y otros elementos de base de datos, organizada por esquema de la base de datos. Seleccione columnas de las tablas o vistas, o especifique los procedimientos almacenados o las funciones con valores de tabla. Limite el número de filas de datos que desea recuperar especificando los criterios de filtro. Personalice el filtro al ejecutarse el informe estableciendo la opción de parámetro.  
  
-   Escriba o pegue una consulta. Use el diseñador de consultas basado en texto para escribir texto [!INCLUDE[tsql](../../includes/tsql-md.md)] directamente, para pegar texto de consulta de otro origen, para especificar consultas complejas que no se pueden generar con el diseñador de consultas relacionales o para escribir expresiones basadas en consultas.  
  
-   Importe una consulta existente de un archivo o informe. Utilice el botón de consulta **Importar** desde cualquier diseñador de consultas para buscar un archivo .sql o .rdl e importar una consulta.  
  
 Para más información, vea [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md) e [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 Se admiten los siguientes modos de consulta:  
  
-   [Texto:](#QueryText) escriba comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   [Procedimiento almacenado:](#QueryStoredProcedure) Elija de una lista de procedimientos almacenados.  
  
###  <a name="QueryText"></a> Usar consultas de tipo Texto  
 En el diseñador de consultas basado en texto, puede escribir comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir los datos de un conjunto de datos. Por ejemplo, la siguiente consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] selecciona todos los nombres de todos los empleados que son asistentes de marketing:  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 Haga clic en el botón **Ejecutar** (**!**) de la barra de herramientas para ejecutar la consulta y mostrar un conjunto de resultados.  
  
 Para parametrizar esta consulta, agregue un parámetro de consulta. Por ejemplo, modifique la cláusula WHERE con la siguiente información:  
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 Al ejecutar la consulta, se crean automáticamente parámetros de informe correspondientes a los parámetros de la consulta. Para obtener más información, vea [Parámetros de consulta](#Parameters) , más adelante en este tema.  
  
  
###  <a name="QueryStoredProcedure"></a> Usar consultas de tipo StoredProcedure  
 Puede especificar un procedimiento almacenado para una consulta del conjunto de datos de una de las maneras siguientes:  
  
-   En el cuadro de diálogo **Propiedades del conjunto de datos** , establezca la opción **Procedimiento almacenado** . Elija de la lista desplegable de procedimientos almacenados y funciones con valores de tabla.  
  
-   En el diseñador de consultas relacionales, en el panel Vista de base de datos, seleccione un procedimiento almacenado o una función con valores de tabla.  
  
-   En el diseñador de consultas basado en texto, seleccione **StoredProcedure** en la barra de herramientas.  
  
 Después de seleccionar un procedimiento almacenado o una función con valores de tabla, puede ejecutar la consulta. Se le solicitarán los valores de los parámetros de entrada. Al ejecutar la consulta, se crean automáticamente parámetros de informe correspondientes a los parámetros de entrada. Para obtener más información, vea [Parámetros de consulta](#Parameters) , más adelante en este tema.  
  
 Se admite solo el primer conjunto de resultados que se recupera para un procedimiento almacenado. Si un procedimiento almacenado devuelve varios conjuntos de resultados, se utiliza el primero.  
  
 Si un procedimiento almacenado incluye un parámetro que tiene un valor predeterminado, puede tener acceso a dicho valor utilizando la palabra clave DEFAULT como valor del parámetro. Si el parámetro de consulta está vinculado a un parámetro de informe, el usuario puede escribir o seleccionar la palabra DEFAULT en el cuadro de entrada del parámetro de informe.  
  
 Para obtener más información, vea [Procedimientos almacenados (motor de base de datos](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)).  
  
  
##  <a name="Parameters"></a> Parámetros  
 Cuando el texto de consulta contiene variables de consulta o procedimientos almacenados con parámetros de entrada, se generan automáticamente los correspondientes parámetros de consulta y parámetros de informe para el informe. El texto de consulta no debe incluir la instrucción DECLARE para cada variable de consulta.  
  
 Por ejemplo, la siguiente consulta SQL crea un parámetro de informe denominado **EmpID**:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 Los parámetros de informe se crean con valores de propiedad predeterminados que quizá necesite modificar. Por ejemplo:  
  
-   De forma predeterminada, cada parámetro de informe es un tipo de datos **Texto**. Si los datos subyacentes son un tipo de datos diferente, debe cambiar el tipo de datos de parámetro.  
  
-   Si selecciona la opción de parámetros de varios valores, debe cambiar manualmente la consulta para comprobar si los valores forman parte de un conjunto mediante el operador **IN** , por ejemplo, `WHERE EmployeeID IN (@EmpID)`.  
  
 Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentarios  
 También puede recuperar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando un tipo de origen de datos ODBC u OLE DB. Para más información, vea [Tipo de conexión OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md) o [Tipo de conexión ODBC &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md).  
  
###### <a name="platform-and-version-information"></a>Información de plataforma y de versión  
 Para obtener más información sobre la compatibilidad de plataformas y de versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar elementos de informe relacionados con datos.  
  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
  
## <a name="see-also"></a>Ver también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
