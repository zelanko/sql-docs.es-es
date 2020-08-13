---
title: Tipo de conexión OLE DB | Microsoft Docs
description: Use la información de este artículo sobre el tipo de conexión OLE DB para obtener información sobre cómo crear un origen de datos.
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 554622ce583bb314609c9000b1398ffbca4b6718
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458230"
---
# <a name="ole-db-connection-type-ssrs"></a>Tipo de conexión OLE DB (SSRS)
  Para incluir los datos de un proveedor de datos OLE DB, debe tener un conjunto de datos basado en un origen de datos de informe de tipo OLE DB. Este tipo de origen de datos integrado se basa en la extensión de procesamiento de datos de OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 OLE DB es una tecnología de acceso a datos que permite a los clientes conectarse a diversos proveedores de datos. Después de seleccionar el tipo de origen de datos OLE DB, debe seleccionar un proveedor de datos concreto. La compatibilidad con características como parámetros y credenciales depende del proveedor de datos que seleccione.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="connection-string"></a><a name="Connection"></a> Cadena de conexión  
 La cadena de conexión para la extensión de procesamiento de datos de OLE DB depende del proveedor de datos que desee. Una cadena de conexión típica contiene pares de nombre/valor admitidos por el proveedor de datos. Por ejemplo, la siguiente cadena de conexión especifica el proveedor OLE DB para la base de datos de AdventureWorks y Native Client de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 La cadena de conexión que use depende del origen de datos externo al que se vaya a conectar. Para establecer propiedades de cadena de conexión específicas de un proveedor de datos, en la página **General** del cuadro de diálogo **Propiedades del origen de datos** , haga clic en el botón **Generar** para abrir el cuadro de diálogo **Propiedades de conexión** . Establezca propiedades de origen de datos extendidas a través del cuadro de diálogo **Propiedades de vínculo de datos** .  
  
 Para más ejemplos de cadenas de conexión, vea [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
  
##  <a name="credentials"></a><a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](specify-credential-and-connection-information-for-report-data-sources.md).  
  
###### <a name="special-characters-in-a-password"></a>Caracteres especiales en una contraseña  
 Si se configura el origen de datos OLE DB para que solicite una contraseña o para que esta se incluya en la cadena de conexión y un usuario especifica una contraseña con caracteres especiales, como signos de puntuación, algunos controladores del origen de datos subyacente no podrán validar los caracteres especiales. Cuando procese el informe, es posible que aparezca un mensaje para indicarle que la contraseña no es válida.  
  
> [!NOTE]  
>  Se recomienda no agregar información de inicio de sesión, como contraseñas, a la cadena de conexión. El cuadro de diálogo **Origen de datos** del Generador de informes incluye una pestaña independiente para especificar las credenciales.  
  
  
##  <a name="parameters"></a><a name="Parameters"></a> Parámetros  
 Algunos proveedores OLE DB admiten parámetros sin nombre y no admiten parámetros con nombre. Los parámetros se pasan por posición mediante un marcador de posición en la consulta. La sintaxis admitida por el proveedor de datos determina el carácter del marcador de posición.  
  
  
##  <a name="remarks"></a><a name="Remarks"></a> Comentarios  
 OLEDB es una tecnología nativa para crear proveedores de datos para orígenes de datos concretos. OLEDB se basa en interfaces COM (Modelo de objetos componentes). OLEDB es una tecnología posterior a ODBC y anterior que los proveedores de datos ADO.NET. Los proveedores de datos de OLEDB se registran con el sistema operativo como cualquier otro componente de COM. Los proveedores de datos de OLEDB están disponibles de Microsoft y otros proveedores. Microsoft también proporciona MSDASQL, un proveedor de datos de OLEDB que establece la comunicación con los controladores ODBC. Para más información, vea [Tipo de conexión ODBC &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md).  
  
 Para recuperar correctamente los datos que desea obtener, deberá proporcionar una sintaxis de consulta que admita el proveedor de datos. La compatibilidad con parámetros varía en función del proveedor de datos. Para obtener más información, consulte los temas específicos del proveedor de datos que seleccione. Por ejemplo:  
  
-   [Proveedor OLE DB de Analysis Services &#40;Analysis Services - Datos multidimensionales&#41;](https://docs.microsoft.com/analysis-services/instances/data-providers-used-for-analysis-services-connections
)  
   
  
-   [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 Para obtener más información sobre proveedores de datos de OLE DB concretos, consulte [Orígenes de datos admitidos por Reporting Services (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="related-sections"></a><a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
