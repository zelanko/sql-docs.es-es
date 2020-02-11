---
title: Tipo de conexión SQL Azure (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c84def6c-e8cf-43d9-9912-098171a7ce79
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cdee6968bc4760688c6497db6d59ad04a33fa033
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107026"
---
# <a name="sql-azure-connection-type-ssrs"></a>Tipo de conexión SQL Azure (SSRS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] es una base de datos relacional hospedada en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nube que se basa en tecnologías. Para incluir en el informe los datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , debe tener un conjunto de datos que se base en un origen de datos de informe de tipo [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Este tipo de origen de datos integrado se basa en la extensión de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] . Utilice este tipo de origen de datos para conectarse y recuperar datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Esta extensión de datos admite parámetros de varios valores, agregados del servidor y credenciales administrados con independencia de la cadena de conexión.  
  
 
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] es similar a una instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la obtención de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] se realiza, con pocas excepciones, de forma idéntica a como se obtienen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Cuando abra una conexión con [!INCLUDE[ssSDS](../../includes/sssds-md.md)], establezca el tiempo de espera de conexión en 30 segundos.  
  
 Para obtener más información, consulte la [documentación de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/).  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a>Cadena de conexión  
 Cuando se conecta a [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se conecta a un objeto de base de datos de la nube. Al igual que las bases de datos de sitio, la base de datos hospedada podría tener varios esquemas con varias tablas, vistas y procedimientos almacenados. Especifique el objeto de base de datos que se va a usar en el diseñador de consultas. Si no especifica una base de datos en la cadena de conexión, puede conectar con la base de datos predeterminada que le asignó el administrador.  
  
 Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En la siguiente cadena de conexión de ejemplo se especifica una base de datos de ejemplo hospedada denominada AdventureWorks.  
  
```  
Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True;  
```  
  
 Además, se usa el cuadro de diálogo **Propiedades de orígenes de datos** para proporcionar credenciales como nombre de usuario y contraseña. Las opciones `User Id` y `Password` se agregan automáticamente a la cadena de conexión, no es necesario escribirlas como parte de dicha cadena.  
  
 Para obtener más información y ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a>Sus  
 No se admite la autenticación Windows (seguridad integrada). Si intenta conectarse a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] utilizando la autenticación de Windows, se producirá un error. 
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] admite solo la autenticación de SQL Server (nombre de usuario y contraseña) y los usuarios deben proporcionar credenciales (inicio de sesión y contraseña) cada vez que se conecten a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Las credenciales deben ser suficientes para tener acceso a la base de datos. En función de la consulta, podría necesitar otros permisos, como los permisos necesarios para ejecutar procedimientos almacenados y tener acceso a tablas. El propietario del origen de datos externo debe configurar credenciales que sean suficientes para proporcionar a los usuarios acceso de solo lectura a los objetos de base de datos que necesiten.  
  
 Desde un cliente de creación de informes, están disponibles las siguientes opciones para especificar las credenciales:  
  
-   Utilizar un nombre de usuario y una contraseña almacenados. Para negociar el salto doble que se produce cuando la base de datos que contiene los datos de informe es distinta del servidor de informes, seleccione opciones para utilizar las credenciales como credenciales de Windows. Puede también decidir suplantar al usuario autenticado tras la conexión al origen de datos.  
  
-   No se necesitan credenciales. Para usar esta opción, debe tener la cuenta de ejecución desatendida configurada en el servidor de informes. Para más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en msdn.microsoft.com.  
  
 Para obtener más información, vea [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [Especifique las credenciales en generador de informes](../specify-credentials-in-report-builder.md).  
  
 
  
##  <a name="Query"></a>Queri  
 Una consulta especifica qué datos se van a recuperar para un conjunto de datos de informe. Las columnas del conjunto de resultados de una consulta rellenan la colección de campos de un conjunto de datos. Si la consulta devuelve varios conjuntos de resultados, el informe procesa solo el primer conjunto de resultados que la consulta recupera. Aunque hay algunas diferencias entre las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDS](../../includes/sssds-md.md)], por ejemplo el tamaño de las bases de datos admitidas, escribir consultas para bases de datos de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], es similar a escribir consultas para bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Algunas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] como BACKUP no se admiten en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], pero no se utilizan en consultas de informe. Para obtener más información, vea [Tipo de conexión de SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md).  
  
 De forma predeterminada, si crea una nueva consulta o abre una consulta existente que puede ser representada en el diseñador gráfico de consultas, este último está disponible. Puede especificar una consulta de varias maneras:  
  
-   Generar una consulta interactivamente. Utilice el diseñador de consultas relacionales que muestra una vista jerárquica de las tablas, las vistas, los procedimientos almacenados y otros elementos de base de datos, organizada por esquema de la base de datos. Seleccione columnas de las tablas o vistas, o especifique los procedimientos almacenados o las funciones con valores de tabla. Limite el número de filas de datos que desea recuperar especificando los criterios de filtro. Personalice el filtro al ejecutarse el informe estableciendo la opción de parámetro.  
  
-   Escriba o pegue una consulta. Use el diseñador de consultas basado en texto para escribir texto [!INCLUDE[tsql](../../includes/tsql-md.md)] directamente, para pegar texto de consulta de otro origen, para especificar consultas complejas que no se pueden generar con el diseñador de consultas relacionales o para escribir expresiones basadas en consultas.  
  
-   Importe una consulta existente de un archivo o informe. Utilice el botón de consulta **Importar** desde cualquier diseñador de consultas para buscar un archivo .sql o .rdl e importar una consulta.  
  
 El diseñador de consultas basado en texto admite los dos modos siguientes:  
  
-   [Texto](#QueryText) de Escriba [!INCLUDE[tsql](../../includes/tsql-md.md)] comandos que seleccionen datos del origen de datos.  
  
-   [Procedimiento almacenado](#QueryStoredProcedure) Elija de una lista de procedimientos almacenados.  
  
 Para más información, vea [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](relational-query-designer-user-interface-report-builder.md) e [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 El diseñador gráfico de consultas usado por [!INCLUDE[ssSDS](../../includes/sssds-md.md)] proporciona compatibilidad integrada con las agrupaciones y agregados para ayudar a los usuarios a escribir consultas que solo recuperen datos de resumen. Las características de lenguaje de [!INCLUDE[tsql](../../includes/tsql-md.md)] son: la cláusula GROUP BY, la palabra clave DISTINCT y agregados, como SUM y COUNT. El diseñador de consultas basado en texto es totalmente compatible con el lenguaje de [!INCLUDE[tsql](../../includes/tsql-md.md)] , incluidas las agrupaciones y los agregados. Para más información sobre [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference) en los Libros en pantalla[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ de ](https://go.microsoft.com/fwlink/?LinkId=141687) en msdn.microsoft.com.  
  
###  <a name="QueryText"></a>Usar texto de tipo de consulta  
 En el diseñador de consultas basado en texto, escriba comandos de [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir los datos de un conjunto de datos. Por ejemplo, la siguiente consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] selecciona todos los nombres de todos los empleados que son asistentes de marketing:  
  
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
  
```  
WHERE HumanResources.Employee.JobTitle = (@JobTitle)  
```  
  
 Al ejecutar la consulta, se crean automáticamente parámetros de informe correspondientes a los parámetros de la consulta. Para obtener más información, vea [Parámetros de consulta](#Parameters) , más adelante en este tema.  
  
  
  
###  <a name="QueryStoredProcedure"></a>Usar el tipo de consulta StoredProcedure  
 Puede especificar un procedimiento almacenado para una consulta del conjunto de datos de una de las maneras siguientes:  
  
-   En el cuadro de diálogo **Propiedades del conjunto de datos** , establezca la opción **Procedimiento almacenado** . Elija de la lista desplegable de procedimientos almacenados y funciones con valores de tabla.  
  
-   En el diseñador de consultas relacionales, en el panel Vista de base de datos, seleccione un procedimiento almacenado o una función con valores de tabla.  
  
-   En el diseñador de consultas basado en texto, seleccione **StoredProcedure** en la barra de herramientas.  
  
 Después de seleccionar un procedimiento almacenado o una función con valores de tabla, puede ejecutar la consulta. Se le solicitarán los valores de los parámetros de entrada. Al ejecutar la consulta, se crean automáticamente parámetros de informe correspondientes a los parámetros de entrada. Para obtener más información, vea [Parámetros de consulta](#Parameters) , más adelante en este tema.  
  
 Se admite solo el primer conjunto de resultados que se recupera para un procedimiento almacenado. Si un procedimiento almacenado devuelve varios conjuntos de resultados, se utiliza el primero.  
  
 Si un procedimiento almacenado incluye un parámetro que tiene un valor predeterminado, puede tener acceso a dicho valor utilizando la palabra clave DEFAULT como valor del parámetro. Si el parámetro de consulta está vinculado a un parámetro de informe, el usuario puede escribir o seleccionar la palabra DEFAULT en el cuadro de entrada del parámetro de informe.  
  
 Para obtener más información sobre los procedimientos almacenados, vea "Procedimientos almacenados (motor de base de datos)" en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?linkid=98335) en msdn.microsoft.com.  
  
  
  
##  <a name="Parameters"></a>Los  
 Cuando el texto de consulta contiene variables de consulta o procedimientos almacenados con parámetros de entrada, se generan automáticamente los correspondientes parámetros de consulta y parámetros de informe para el informe. El texto de consulta no debe incluir la instrucción DECLARE para cada variable de consulta.  
  
 Por ejemplo, la siguiente consulta SQL crea un parámetro de informe denominado `EmpID`:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 De forma predeterminada, cada parámetro de informe tiene el tipo de datos Texto y un conjunto de datos creado automáticamente para proporcionar una lista desplegable de valores disponibles. Una vez creados los parámetros de informe, puede suceder que tenga que cambiar los valores predeterminados. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
  
##  Comentarios para <a name="Remarks"></a>  
  
###### <a name="alternate-data-extensions"></a>Extensiones de datos alternativas  
 También puede recuperar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando un tipo de origen de datos ODBC. No se admite la conexión a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] mediante OLE DB.  
  
 Para más información, vea [Tipo de conexión ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md).  
  
###### <a name="platform-and-version-information"></a>Información de plataforma y de versión  
 Para obtener más información sobre la compatibilidad de plataformas y de versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los Libros en pantalla[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ de ](https://go.microsoft.com/fwlink/?linkid=121312).  
  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de DataSet compartido o un conjunto de &#40;incrustado Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a>Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar elementos de informe relacionados con datos.  
  
 [Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación de en los [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312)de.  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
