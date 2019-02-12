---
title: Tipo de conexión de Oracle (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b1b083ab1da347d3aa90b1eff8480b14bac8350c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027546"
---
# <a name="oracle-connection-type-ssrs"></a>Tipo de conexión de Oracle (SSRS)
  Para utilizar en el informe los datos de una base de datos de Oracle, debe tener un conjunto de datos basado en un origen de datos de informe de tipo Oracle. Este tipo de origen de datos integrado está basado en el proveedor administrado de .NET Framework para Oracle y requiere un componente de software del cliente Oracle.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones detalladas, consulte [agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el siguiente ejemplo de cadena de conexión, se especifica una base de datos de Oracle en el servidor denominado "Oracle9" mediante Unicode. El nombre del servidor debe coincidir con el nombre de instancia del servidor de Oracle definido en el archivo de configuración Tnsnames.ora.  
  
```  
Data Source="Oracle9"; Unicode="True"  
```  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para obtener más información, consulte [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [especificar credenciales en Generador de informes](../specify-credentials-in-report-builder.md).  
  

  
##  <a name="Query"></a> Consultas  
 Para crear un conjunto de datos, se puede seleccionar un procedimiento almacenado en una lista desplegable o se puede crear una consulta SQL. Para generar una consulta, debe usar el diseñador de consultas basado en texto. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 Puede especificar los procedimientos almacenados que solo devuelven un conjunto de resultados. No se admiten las consultas basadas en cursor.  
  
##  <a name="Parameters"></a> Parámetros  
 Si la consulta incluye las variables de consulta, se generan automáticamente los parámetros de informe correspondientes. Esta extensión admite los parámetros con nombre. En Oracle versión 9 o posterior, se admiten los parámetros de varios valores.  
  
 Los parámetros de informe se crean con valores de propiedad predeterminados que quizá necesite modificar. Por ejemplo, los parámetro de informe son un tipo de datos **Texto**. Una vez creados los parámetros de informe, podría suceder que tenga que cambiar los valores predeterminados. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  

  
##  <a name="Remarks"></a> Comentarios  
 Antes de que pueda conectar con un origen de datos de Oracle, el administrador del sistema debe tener instalada la versión del proveedor de datos .NET para Oracle que permite la recuperación de datos desde la base de datos de Oracle. Este proveedor de datos debe estar instalado en el mismo equipo que el Generador de informes, además de en el servidor de informes.  
  
 Para obtener más información, vea:  
  
-   Para obtener más información, vea[Uso del proveedor de datos de .NET Framework para Oracle](https://go.microsoft.com/fwlink/?LinkId=112314) en msdn.microsoft.com  
  
-   [Cómo usar Reporting Services para tener acceso a un origen de datos de Oracle y configurarlo](https://support.microsoft.com/kb/834305)  
  
-   [Cómo agregar permisos para la entidad de seguridad NETWORK SERVICE](https://support.microsoft.com/kb/870668)  
  
###### <a name="alternate-data-extensions"></a>Extensiones de datos alternativas  
 También puede recuperar los datos de una base de datos de Oracle utilizando un tipo de origen de datos OLE DB. Para obtener más información, vea [Tipo de conexión OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
###### <a name="report-models"></a>Modelos de informe  
 También se pueden crear modelos basados en una base de datos de Oracle.  
  
###### <a name="platform-and-version-information"></a>Información de plataforma y de versión  
 Para obtener más información sobre la compatibilidad de plataformas y de versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  

  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  

  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
