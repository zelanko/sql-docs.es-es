---
title: "Tipo de conexión de OLE DB (SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 294cddfd0f3cc35c2f4a3b2b6861bc062648d849
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="ole-db-connection-type-ssrs"></a>Tipo de conexión OLE DB (SSRS)
  Para incluir los datos de un proveedor de datos OLE DB, debe tener un conjunto de datos basado en un origen de datos de informe de tipo OLE DB. Este tipo de origen de datos integrado se basa en la extensión de procesamiento de datos de OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 OLE DB es una tecnología de acceso a datos que permite a los clientes conectarse a diversos proveedores de datos. Después de seleccionar el tipo de origen de datos OLE DB, debe seleccionar un proveedor de datos concreto. La compatibilidad con características como parámetros y credenciales depende del proveedor de datos que seleccione.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 La cadena de conexión para la extensión de procesamiento de datos de OLE DB depende del proveedor de datos que desee. Una cadena de conexión típica contiene pares de nombre/valor admitidos por el proveedor de datos. Por ejemplo, la siguiente cadena de conexión especifica el proveedor OLE DB para la base de datos de AdventureWorks y Native Client de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 La cadena de conexión que use depende del origen de datos externo al que se vaya a conectar. Para establecer propiedades de cadena de conexión específicas de un proveedor de datos, en la página **General** del cuadro de diálogo **Propiedades del origen de datos** , haga clic en el botón **Generar** para abrir el cuadro de diálogo **Propiedades de conexión** . Establezca propiedades de origen de datos extendidas a través del cuadro de diálogo **Propiedades de vínculo de datos** .  
  
 Para obtener ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) o [Especificar credenciales en el Generador de informes](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
###### <a name="special-characters-in-a-password"></a>Caracteres especiales en una contraseña  
 Si se configura el origen de datos OLE DB para que solicite una contraseña o para que esta se incluya en la cadena de conexión y un usuario especifica una contraseña con caracteres especiales, como signos de puntuación, algunos controladores del origen de datos subyacente no podrán validar los caracteres especiales. Cuando procese el informe, es posible que aparezca un mensaje para indicarle que la contraseña no es válida.  
  
> [!NOTE]  
>  Se recomienda no agregar información de inicio de sesión, como contraseñas, a la cadena de conexión. El cuadro de diálogo **Origen de datos** del Generador de informes incluye una pestaña independiente para especificar las credenciales.  
  
  
##  <a name="Parameters"></a> Parámetros  
 Algunos proveedores OLE DB admiten parámetros sin nombre y no admiten parámetros con nombre. Los parámetros se pasan por posición mediante un marcador de posición en la consulta. La sintaxis admitida por el proveedor de datos determina el carácter del marcador de posición.  
  
  
##  <a name="Remarks"></a> Comentarios  
 OLEDB es una tecnología nativa para crear proveedores de datos para orígenes de datos concretos. OLEDB se basa en interfaces COM (Modelo de objetos componentes). OLEDB es una tecnología posterior a ODBC y anterior que los proveedores de datos ADO.NET. Los proveedores de datos de OLEDB se registran con el sistema operativo como cualquier otro componente de COM. Los proveedores de datos de OLEDB están disponibles de Microsoft y otros proveedores. Microsoft también proporciona MSDASQL, un proveedor de datos de OLEDB que establece la comunicación con los controladores ODBC. Para obtener más información, vea [tipo de conexión ODBC &#40; SSRS &#41; ](../../reporting-services/report-data/odbc-connection-type-ssrs.md).  
  
 Para recuperar correctamente los datos que desea obtener, deberá proporcionar una sintaxis de consulta que admita el proveedor de datos. La compatibilidad con parámetros varía en función del proveedor de datos. Para obtener más información, consulte los temas específicos del proveedor de datos que seleccione. Por ejemplo:  
  
-   [Proveedor OLE DB de Analysis Services &#40;Analysis Services - Datos multidimensionales&#41;](http://msdn.microsoft.com/library/cdeecd50-1d91-4162-a4a2-01c7799b02a8)  
  
-   [Uso del proveedor de datos de .NET Framework para Oracle](http://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 Para obtener más información sobre proveedores de datos de OLE DB concretos, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Informe incrusta los conjuntos de datos y conjuntos de datos compartidos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección de campos de conjunto de datos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40; El generador de informes y el Diseñador de informes &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, grupo y ordenar los datos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
