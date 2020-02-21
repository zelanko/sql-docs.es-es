---
title: Tipo de conexión de Oracle (SSRS, Power BI Report Server y Generador de informes) | Microsoft Docs
ms.date: 01/16/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f6918d240a6da7f961899d1a4cb71996bbec9ec6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "76259403"
---
# <a name="oracle-connection-type-ssrs-power-bi-report-server-and-report-builder"></a>Tipo de conexión de Oracle (SSRS, Power BI Report Server y Generador de informes)

Para utilizar en el informe los datos de una base de datos de Oracle, debe tener un conjunto de datos basado en un origen de datos de informe de tipo Oracle. Este tipo de origen de datos integrado usa el proveedor de datos de Oracle directamente y requiere un componente de software del cliente Oracle. En este artículo se explica cómo descargar e instalar controladores para Reporting Services, Power BI Report Server y Generador de informes.

## <a name="64-bit-drivers-for-the-report-servers"></a>Controladores de 64 bits para los servidores de informes

Tanto Power BI Report Server como SQL Server Reporting Services 2016 y 2017 usan ODP.NET administrado. Los pasos siguientes solo son necesarios para cuando se usan los controladores de 18x más recientes. Se supone que instaló los archivos en c:\oracle64.

1. En el sitio de descarga de Oracle, instale [Oracle Universal Installer (OUI) de ODAC para Oracle de 64 bits](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdeploy-4242173.html). 
2. Registre el cliente de ODP.NET administrado en GAC:  C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
3. Agregue las entradas del cliente de ODP.NET administrado al archivo machine.config:  C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /productversion:4.122.18.3

### <a name="power-bi-reports-use-unmanaged-odpnet"></a>Los informes de Power BI usan ODP.NET no administrado

Los informes de Power BI usan **ODP.NET no administrado**. Siga estos pasos para registrar ODP.NET no administrado:

1. Registre el cliente de ODP.NET no administrado en GAC:

   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
2. Agregue las entradas del cliente de ODP.NET no administrado al archivo machine.config:

   C:\oracle64\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /productversion:4.122.18.3
 
## <a name="32-bit-drivers-for-report-builder"></a>Controladores de 32 bits para Generador de informes

Los pasos siguientes solo son necesarios para cuando se usan los controladores de 18x más recientes. Se supone que instaló los archivos en c:\oracle32.

1. En el sitio de descarga de Oracle, instale [Oracle Universal Installer (OUI) de ODAC para Oracle de 32 bits](https://www.oracle.com/technetwork/topics/dotnet/downloads/odacdev-4242174.html).
2. Registre el cliente de ODP.NET administrado en GAC:  C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\managed\common\Oracle.ManagedDataAccess.dll
3. Agregue las entradas del cliente de ODP.NET administrado al archivo machine.config:  C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odpm /frameworkversion:v4.0.30319 /productversion:4.122.18.3

### <a name="power-bi-reports-use-unmanaged-odpnet"></a>Los informes de Power BI usan ODP.NET no administrado  

Los informes de Power BI usan **ODP.NET no administrado**. Siga estos pasos para registrar ODP.NET no administrado:

1. Registre el cliente de ODP.NET no administrado en GAC:

   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:gac /providerpath:C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll
2. Agregue las entradas del cliente de ODP.NET no administrado al archivo machine.config:

   C:\oracle32\product\18.0.0\client_1\odp.net\bin\4\OraProvCfg.exe /action:config /force /product:odp /frameworkversion:v4.0.30319 /productversion:4.122.18.3
 

 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el siguiente ejemplo de cadena de conexión, se especifica una base de datos de Oracle en el servidor denominado "Oracle18" mediante Unicode. El nombre del servidor debe coincidir con el nombre de instancia del servidor de Oracle definido en el archivo de configuración Tnsnames.ora.  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 Para más ejemplos de cadenas de conexión, consulte [Creación de cadenas de conexión de datos - Generador de informes y SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
 Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](specify-credential-and-connection-information-for-report-data-sources.md).  
  
  
##  <a name="Query"></a> Consultas  
 Para crear un conjunto de datos, se puede seleccionar un procedimiento almacenado en una lista desplegable o se puede crear una consulta SQL. Para generar una consulta, debe usar el diseñador de consultas basado en texto. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 Puede especificar los procedimientos almacenados que solo devuelven un conjunto de resultados. No se admiten las consultas basadas en cursor.  
  
##  <a name="Parameters"></a> Parámetros  
 Si la consulta incluye las variables de consulta, se generan automáticamente los parámetros de informe correspondientes. Esta extensión admite los parámetros con nombre. En Oracle versión 9 o posterior, se admiten los parámetros de varios valores.  
  
 Los parámetros de informe se crean con valores de propiedad predeterminados que quizá necesite modificar. Por ejemplo, los parámetro de informe son un tipo de datos **Texto**. Una vez creados los parámetros de informe, podría suceder que tenga que cambiar los valores predeterminados. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentarios  
 Antes de que pueda conectar con un origen de datos de Oracle, el administrador del sistema debe tener instalada la versión del proveedor de datos .NET para Oracle que permite la recuperación de datos desde la base de datos de Oracle. Este proveedor de datos debe estar instalado en el mismo equipo que el Generador de informes, además de en el servidor de informes.  
  
 Para más información, consulte los siguientes artículos.  
  
-   [Cómo usar Reporting Services para tener acceso a un origen de datos de Oracle y configurarlo](https://support.microsoft.com/kb/834305)  
-   [Cómo agregar permisos para la entidad de seguridad NETWORK SERVICE](https://support.microsoft.com/kb/870668)  
  
### <a name="alternate-data-extensions"></a>Extensiones de datos alternativas 
 
 También puede recuperar los datos de una base de datos de Oracle utilizando un tipo de origen de datos OLE DB. Para obtener más información, vea [Tipo de conexión OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md).  

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions" 
### <a name="report-models"></a>Modelos de informe  

 También se pueden crear modelos basados en una base de datos de Oracle.  
::: moniker-end
   
### <a name="platform-and-version-information"></a>Información de plataforma y de versión  

 Para más información sobre la compatibilidad con plataformas y versiones, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  

  
## <a name="see-also"></a>Consulte también

 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
