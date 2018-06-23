---
title: Tipo de conexión Almacenamiento de datos paralelo de SQL Server (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3925fd3d-2aa1-4768-96ad-cfc2c0ba9283
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7a8ce540cb3ecf555e5abc22a1927482409bc582
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106281"
---
# <a name="sql-server-parallel-data-warehouse-connection-type-ssrs"></a>Tipo de conexión Almacenamiento de datos paralelo de SQL Server (SSRS)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] es un dispositivo de almacenamiento de datos escalable que ofrece rendimiento y escalabilidad mediante un procesamiento paralelo masivo. [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] usa [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] bases de datos de almacenamiento de datos y procesamiento distribuido.  
  
 El dispositivo particiona tablas de base de datos grandes en varios nodos físicos, cada uno de los cuales ejecuta su propia instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Cuando un informe se conecta a [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] para recuperar datos de informes, se conecta al nodo de control que administra el procesamiento de consultas, en la [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] dispositivo. Una vez realizada la conexión, no existirá ninguna diferencia entre trabajar con una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que esté o no dentro de un entorno de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)].  
  
 Para incluir los datos de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] en el informe, debe tener un conjunto de datos que se basa en un origen de datos de informe de tipo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] almacenamiento de datos paralelos. Este tipo de origen de datos integrado se basa en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] extensión de datos de almacenamiento de datos paralelos. Utilice este tipo de origen de datos para conectarse y recuperar datos de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)].  
  
 Esta extensión de datos admite parámetros de varios valores, agregados del servidor y credenciales administrados con independencia de la cadena de conexión.  
  
 Para obtener más información, vea el sitio web relativo al [Almacenamiento de datos paralelo de SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkId=150895).  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones detalladas, consulte [agregar y comprobar una conexión de datos o un origen de datos &#40;el generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Al conectarse a [!INCLUDE[ssDW](../../../includes/ssdw-md.md)], lo hace a un objeto de base de datos dentro de un dispositivo [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] . Especifique el objeto de base de datos que se va a usar en el diseñador de consultas. Si no especifica una base de datos en la cadena de conexión, puede conectar con la base de datos predeterminada que le asignó el administrador. Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. El siguiente ejemplo de cadena de conexión especifica la base de datos de ejemplo, **CustomerSales**, en la [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] dispositivo:  
  
```  
HOST=<IP address>; database= CustomerSales; port=<port>  
```  
  
 Además, utilice el cuadro de diálogo **Propiedades de orígenes de datos** para proporcionar credenciales, como el nombre de usuario y la contraseña. Las opciones `User Id` y `Password` se anexan automáticamente a la cadena de conexión; no necesita escribirlos como parte de la cadena de conexión. La interfaz de usuario también proporciona opciones para especificar la dirección IP del nodo de control en el [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] dispositivo y el número de puerto. De forma predeterminada, el puerto es el 17000. El administrador puede configurar el puerto y su cadena de conexión puede utilizar un número de puerto diferente.  
  
 Para obtener más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciales  
 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] proporciona su propia tecnología de seguridad para implementar y almacenar nombres de usuario y contraseñas. No podrá utilizar la autenticación de Windows. Si intenta conectarse a [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] utilizando la autenticación de Windows, se producirá un error.  
  
 Las credenciales deben ser suficientes para tener acceso a la base de datos. En función de la consulta, podría necesitar otros permisos, como los permisos necesarios para tener acceso a las tablas y a las vistas. El propietario del origen de datos externo debe configurar credenciales que sean suficientes para proporcionar a los usuarios acceso de solo lectura a los objetos de base de datos que necesiten.  
  
 Desde un cliente de creación de informes, están disponibles las siguientes opciones para especificar las credenciales:  
  
-   Utilizar un nombre de usuario y una contraseña almacenados. Para negociar el salto doble que se produce cuando la base de datos que contiene los datos de informe es distinta del servidor de informes, seleccione opciones para utilizar las credenciales como credenciales de Windows. Puede también decidir suplantar al usuario autenticado tras la conexión al origen de datos.  
  
-   No se necesitan credenciales. Para usar esta opción, debe tener la cuenta de ejecución desatendida configurada en el servidor de informes. Para más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en la [documentación de Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) en msdn.microsoft.com.  
  
 Para obtener más información, consulte [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [especificar credenciales en el generador de informes](../specify-credentials-in-report-builder.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Query"></a> Consultas  
 Una consulta especifica qué datos se van a recuperar para un conjunto de datos de informe.  
  
 Las columnas del conjunto de resultados de una consulta rellenan la colección de campos de un conjunto de datos. Si la consulta devuelve varios conjuntos de resultados, el informe procesa solo el primer conjunto de resultados que una consulta recupera. De forma predeterminada, si crea una nueva consulta o abre una consulta existente que puede ser representada en el diseñador gráfico de consultas, este último está disponible. Puede especificar una consulta de varias maneras:  
  
-   Generar una consulta interactivamente. Utilice el diseñador de consultas relacionales que muestra una vista jerárquica de las tablas, las vistas y otros elementos de base de datos, organizada por esquema de la base de datos. Seleccione columnas de las tablas o de las vistas. Limite el número de filas de datos que se recuperarán especificando criterios de filtro, agrupación y agregados. Personalice el filtro al ejecutarse el informe estableciendo la opción de parámetro.  
  
-   Escriba o pegue una consulta. Use el Diseñador de consultas basado en texto para especificar [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] texto directamente, para pegar texto de consulta de otro origen, para especificar consultas complejas que no se puede crear mediante el Diseñador de consultas relacionales, o para escribir expresiones basadas en consultas.  
  
-   Importe una consulta existente de un archivo o informe. Utilice el botón de consulta **Importar** desde cualquier diseñador de consultas para buscar un archivo .sql o .rdl e importar una consulta.  
  
 Para más información, vea [Interfaz de usuario del Diseñador de consultas relacionales &#40;Generador de informes&#41;](relational-query-designer-user-interface-report-builder.md) e [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 El diseñador de consultas basado en texto admite el modo [Texto](#QueryText) en el que el usuario escribe los comandos de [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] que seleccionan datos del origen de datos.  
  
-   [Texto](#QueryText)  
  
 Utilice [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] con [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] y [!INCLUDE[tsql](../../../includes/tsql-md.md)] con [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Los dos dialectos del lenguaje SQL son muy parecidos. Las consultas escritas para el tipo de conexión a un origen de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pueden utilizar normalmente para el tipo de conexión a un origen de datos de [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)].  
  
 Una consulta que recupere datos de informe de una base de datos grande, por ejemplo un almacenamiento de datos como [!INCLUDE[ssDW](../../../includes/ssdw-md.md)], podría generar un conjunto de resultados con un número muy grande de filas a menos que se agreguen y resuman los datos para reducir el número de filas que la consulta devuelve. Puede escribir consultas que incluyan agregados y agrupaciones mediante el diseñador gráfico de consultas o el diseñador de consultas basado en texto.  
  
 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] admite la cláusula, palabra clave y agregados que el Diseñador de consultas proporciona para resumir los datos.  
  
 El diseñador gráfico de consultas usado por [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] proporciona compatibilidad integrada con las agrupaciones y agregados para ayudar a los usuarios a escribir consultas que solo recuperen datos de resumen. El [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] son características del lenguaje: el grupo por cláusulas, palabra clave DISTINCT y agregados, como SUM y COUNT. El Diseñador de consultas basado en texto proporciona compatibilidad completa para el [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] lenguaje, incluida la agrupación y agregados.  
  
 Para más información sobre [!INCLUDE[tsql](../../../includes/tsql-md.md)], vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference) en los [Libros en pantalla](http://go.microsoft.com/fwlink/?LinkId=141687) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en msdn.microsoft.com.  
  
###  <a name="QueryText"></a> Usar consultas de tipo Texto  
 En el diseñador de consultas basado en texto, escriba comandos de [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] para definir los datos de un conjunto de datos. Las consultas que utilizan para recuperar datos de [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] son las mismas que las que se utilizan para recuperar datos de instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no se ejecuta dentro de un [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] aplicación. Por ejemplo, la siguiente [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] consulta selecciona todos los nombres de todos los empleados que son asistentes de marketing:  
  
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
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Parameters"></a> Parámetros  
 Cuando el texto de consulta contiene variables de consulta o procedimientos almacenados con parámetros de entrada, se generan automáticamente los correspondientes parámetros de consulta y parámetros de informe para el informe. El texto de consulta no debe incluir la instrucción DECLARE para cada variable de consulta.  
  
 Por ejemplo, la siguiente consulta SQL crea un parámetro de informe denominado `EmpID`:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 De forma predeterminada, cada parámetro de informe tiene el tipo de datos Texto y un conjunto de datos creado automáticamente para proporcionar una lista desplegable de valores disponibles. Una vez creados los parámetros de informe, podría suceder que tenga que cambiar los valores predeterminados. Para obtener más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Remarks"></a> Comentarios  
  
###### <a name="platform-and-version-information"></a>Información de plataforma y de versión  
 Para obtener más información sobre la compatibilidad de plataformas y de versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;el generador de informes SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar elementos de informe relacionados con datos.  
  
 [Agregar datos a un informe &#40;el generador de informes SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
