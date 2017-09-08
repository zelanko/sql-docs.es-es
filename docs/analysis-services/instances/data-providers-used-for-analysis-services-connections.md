---
title: Proveedores de datos utilizados para las conexiones de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d6cd6ad8d29ba92b2da6149874b998f54c32a4af
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="data-providers-used-for-analysis-services-connections"></a>Proveedores de datos usados para conexiones de Analysis Services
  Analysis Services proporciona tres proveedores de datos para el acceso al servidor y a datos. Todas las aplicaciones que se conectan a Analysis Services lo hacen mediante uno de estos proveedores. Dos de los proveedores, ADOMD.NET y Objetos de administración de Analysis Services (AMO), son proveedores de datos administrados. El proveedor OLE DB de Analysis Services (MSOLAP DLL) es un proveedor de datos nativo.  
  
 En las organizaciones que ejecutan varias versiones de Analysis Services, puede que tenga que instalar versiones más recientes de los proveedores de datos en las estaciones de trabajo de los usuarios que se conectan a datos de Analysis Services. La conexiones a las versiones más recientes de Analysis Services requieren proveedores de datos de la misma versión principal. Por ejemplo, para conectarse a [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], todas las estaciones de trabajo necesitan tener un proveedor de datos de la misma versión. Aunque Excel instala los proveedores de datos que necesita para conectarse, ese proveedor puede estar obsoleto con respecto a las instancias de Analysis Services que usa.  
  
 Este tema contiene las siguientes secciones:  
  
 [Cómo determinar la versión del servidor](#bkmk_ServVers)  
  
 [Cómo determinar la versión de los proveedores de datos de Analysis Services](#bkmk_LibUpdate)  
  
 [Dónde obtener versiones más recientes de los proveedores de datos](#bkmk_downloadsite)  
  
 [Proveedor OLE DB de Analysis Services](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="bkmk_ServVers"></a> Cómo determinar la versión del servidor  
 Conocer la versión de la instancia de Analysis Services le ayudará a determinar si necesita instalar versiones más recientes de los proveedores de datos en las estaciones de trabajo de la organización.  
  
-   En SQL Server Management Studio, conéctese a la instancia de Analysis Services. También puede ver información sobre la versión en **Propiedades del servidor** > **General** > **Versión**.  
  
 El número de compilación principal de la versión inicial de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] es 13.0.1601.5.  
  
  
##  <a name="bkmk_LibUpdate"></a> Cómo determinar la versión de los proveedores de datos de Analysis Services  
 Los proveedores de datos se instalan con Analysis Services, así como con las aplicaciones cliente que habitualmente se conectan a bases de datos de Analysis Services, como Excel.  
  
 Office 2010 instala proveedores de datos desde SQL Server 2008. Office 2013 instala proveedores de datos desde SQL Server 2012, etc. Si está usando varias versiones de Office o SQL Server y la disponibilidad de las características o las conexiones no son lo que esperaba, quizás necesite instalar una versión más reciente de los proveedores de datos. Puede ejecutar varias versiones principales de cada proveedor de datos en paralelo en el mismo equipo.  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>Buscar la versión de archivo del proveedor OLEDB  
  
1.  Vaya a \Archivos de programa\Microsoft Analysis Services\AS OLEDB\130.  
  
2.  Haga clic con el botón derecho en **msolap130.dll** > **Propiedades** > **Detalles**.  
  
 Si no encuentra el archivo en esta ubicación, o si la ruta de acceso de la carpeta incluye AS OLEDB\110 or AS OLEDB\90, está usando una biblioteca antigua y debe instalar una versión más reciente (AS OLEDB\11) para conectarse a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>Buscar la versión de archivo de ADOMD.NET y AMO  
  
1.  Vaya a C:\Windows\Assembly.  
  
2.  Haga clic con el botón derecho en Microsoft.AnalysisServices.AdomdClient y, después, haga clic en **Propiedades**. Haga clic en **Versión**.  
  
     En el caso de AMO, haga clic con el botón secundario en Microsoft.AnalysisServices.  
  
##  <a name="bkmk_downloadsite"></a> Dónde obtener versiones más recientes de los proveedores de datos  
 La versión instalada en el equipo cliente debe coincidir con la versión principal del servidor que proporciona los datos. Si la instalación del servidor es más reciente que los proveedores de datos instalados en las estaciones de trabajo de la red, quizás tenga que instalar bibliotecas más recientes.  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>Buscar los proveedores de datos en el sitio de descarga  
  
1.  Vaya al [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52676).  
  
2.  Haga clic en **Descargar**. ADOMD.NET, el proveedor OLE DB y AMO se incluyen en la lista como un paquete instalable. Por ejemplo, SQL_AS_OLEDB.msi. Todas las bibliotecas están disponibles en versiones de 32 o de 64 bits. Los servidores y las estaciones de trabajo más modernas que ejecuten un sistema operativo de 64 bits necesitarán la versión de 64 bits.  
  
##  <a name="bkmk_OLE"></a> Proveedor OLE DB de Analysis Services  
 El proveedor OLE DB de Analysis Services es el proveedor nativo para las conexiones de base de datos de Analysis Services. ADOMD.NET y AMO usan indirectamente MSOLAP, delegando las solicitudes de conexión al proveedor de datos. También puede llamar al proveedor OLE DB directamente desde el código de aplicación, lo que podría hacer si los requisitos de la solución impiden el uso de una API administrada.  
  
 El programa de instalación de SQL Server, Excel y otras aplicaciones que se usan con frecuencia para tener acceso a las bases de datos de Analysis Services instalan automáticamente el proveedor OLE DB para Analysis Services. También puede instalarlo manualmente si lo descarga desde el centro de descarga. De forma predeterminada, el proveedor puede encontrarse en la carpeta \Archivos de programa\Microsoft Analysis Services. El proveedor debe instalarse en cualquier estación de trabajo que se use para tener acceso a datos de Analysis Services.  
  
 MSOLAP130.dll es la versión del proveedor OLE DB para Analysis Services que se incluye en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Otras versiones anteriores recientes incluyen MSOLAP110.dll (para SQL Server 2008 y SQL Server 2008 R2) y MSOLAP90.dll (para SQL Server 2005).  
  
 Los proveedores OLE DB suelen especificarse en las cadenas de conexión. Una cadena de conexión de Analysis Services usa una nomenclatura diferente para hacer referencia al proveedor OLE DB: MSOLAP. \<versión > .dll  
  
 MSOLAP.5.dll es el proveedor OLE DB para Analysis Services que se instala con Excel 2013. Las versiones anteriores, como MSOLAP.4.dll o MSOLAP.3.dll, se encuentran a menudo en estaciones de trabajo que ejecutan versiones anteriores de Excel. Algunas características de Analysis Services, como el complemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], necesitan versiones específicas del proveedor OLE DB. Para más información, vea [Propiedades de cadena de conexión &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
##  <a name="bkmk_ADOMD"></a> ADOMD.NET  
 ADOMD.NET es un proveedor de datos administrado que se usa para consultar datos de Analysis Services. Excel emplea ADOMD.NET al conectarse a un cubo concreto de Analysis Services. La cadena de conexión que ve en Excel corresponde a una conexión de ADOMD.NET.  
  
 El programa de instalación de SQL Server instala ADOMD.NET y lo usan las aplicaciones cliente de SQL Server para conectarse a Analysis Services. Office instala esta biblioteca para admitir conexiones de datos de Excel. Como ocurre con otros proveedores de datos incluidos en SQL Server, puede redistribuir ADOMD.NET si usa la biblioteca en código personalizado. También puede descargarlo e instalarlo de forma manual para obtener la versión más reciente (vea [Cómo determinar la versión de los proveedores de datos de Analysis Services](#bkmk_LibUpdate) en este tema).  
  
 Para comprobar la información de la versión de archivos, busque ADOMD.NET en la memoria caché de ensamblados global, donde se muestra como `Microsoft.AnalysisServices.AdomdClient`.  
  
 Al conectarse a una base de datos, las propiedades de cadena de conexión para las tres bibliotecas son iguales en gran medida. Casi todas las cadenas de conexión que defina para ADOMD.NET (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>) funcionarán también para AMO y el proveedor OLE DB de Analysis Services. Para más información, vea [Propiedades de cadena de conexión &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
 Para obtener más información sobre la conexión mediante programación, vea [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md).  
  
##  <a name="blkmk_AMO"></a> AMO  
 AMO es un proveedor de datos administrado que se usa para la administración del servidor y la definición de datos. Por ejemplo, SQL Server Management Studio usa AMO para conectarse a Analysis Services.  
  
 El programa de instalación de SQL Server instala AMO y lo usan las aplicaciones cliente de SQL Server para conectarse a Analysis Services. También puede descargarlo e instalarlo de forma manual con AMO en código personalizado (vea [Cómo determinar la versión de los proveedores de datos de Analysis Services](#bkmk_LibUpdate) en este tema). AMO puede encontrarse en la memoria caché global de ensamblados global, como `Microsoft.AnalysisServices`.  
  
 Una conexión a través de AMO es suele ser mínima, que consta de "origen de datos =\<servername >". Una vez establecida una conexión, use la API para trabajar con colecciones de base de datos y los objetos principales. Tanto SSDT como SSMS usan AMO para conectarse a una instancia de Analysis Services.  
  
 Para obtener más información sobre la conexión mediante programación, vea [Programming AMO Fundamental Objects](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
