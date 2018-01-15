---
title: Componentes del flujo de ODBC | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 514818fce9654a720dac0a0721697b30bdcab787
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="odbc-flow-components"></a>Componentes del flujo de ODBC
  En este tema se describen los conceptos necesarios para crear un flujo de datos ODBC mediante [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 El conector para conectividad abierta de base de datos (ODBC) para [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ayuda a los desarrolladores de SSIS a crear fácilmente paquetes que cargan y descargan los datos de las bases de datos que admiten ODBC.  
  
 El conector ODBC se ha diseñado para lograr un rendimiento óptimo al cargar o descargar datos en una base de datos que admite ODBC en el contexto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
## <a name="benefits"></a>Ventajas  
 El origen ODBC y el destino ODBC para [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] aportan valor al uso de SSIS en los proyectos que se ocupan de cargar o descargar los datos en las bases de datos que admiten ODBC.  
  
 El origen y el destino ODBC permiten la integración de datos de alto rendimiento con las bases de datos habilitadas para ODBC. Ambos componentes pueden configurarse para trabajar con enlaces de matriz de parámetros de fila para los proveedores ODBC con una gran funcionalidad que admiten este modo de enlace y con enlaces de parámetros de una sola fila para los proveedores ODBC con pocas funciones.  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>Introducción al origen y el destino ODBC  
 Para configurar paquetes que usan [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], debe asegurarse de que dispone de lo siguiente.  
  
-   [Origen ODBC](../../integration-services/data-flow/odbc-source.md)  
  
-   [Destino ODBC](../../integration-services/data-flow/odbc-destination.md)  
  
 El origen ODBC y el destino ODBC proporcionan una forma sencilla de descargar, cargar y transferir los datos desde una base de datos de origen que admite ODBC a una base de datos de destino que admite ODBC.  
  
 Para usar el origen o el destino para cargar o descargar datos, abra un nuevo proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Después, arrastre el origen o el destino a la superficie de diseño de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   El componente de origen ODBC lee los datos de la base de datos que admite ODBC de origen.  
  
 Puede conectar el origen ODBC a un destino o transformar el componente que admite SSIS.  
  
 **Vea también:**  
  
 Origen ODBC  
  
 Editor de origen de ODBC (página Administrador de conexiones)  
  
 Editor de origen de ODBC (página Salida de error)  
  
-   El destino ODBC carga los datos en una base de datos que admite ODBC. Puede conectar el destino a un origen o transformar el componente que admite SSIS.  
  
 **Vea también:**  
  
 Destino ODBC  
  
 Editor de destino de ODBC (página Administrador de conexiones)  
  
 Editor de destinos de ODBC (página Salida de error)  
  
## <a name="operating-scenarios"></a>Escenarios operativos  
 En esta sección se describen algunos de los usos principales de los componentes de origen y de destino ODBC.  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>Copia masiva de datos de tablas de SQL Server a alguna tabla de base de datos que admite ODBC  
 Puede usar los componentes para copiar los datos de forma masiva de una o más tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una única tabla de base de datos que admite ODBC.  
  
 El ejemplo siguiente muestra cómo crear una tarea Flujo de datos SSIS que extrae los datos de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los carga en una tabla DB2.  
  
-   Cree un proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   Cree un administrador de conexiones OLE DB que se conecta a la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene los datos que desea copiar.  
  
-   Cree un administrador de conexiones ODBC que use un controlador DB2 ODBC instalado localmente con un DSN que señala a una base de datos DB2 local o remota. Esta base de datos es donde se cargan los datos de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Arrastre un origen OLE DB a la superficie de diseño, después de configurar el origen para obtener los datos de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la tabla con los datos que se van a extraer. Use el administrador de conexiones OLE DB que creó anteriormente.  
  
-   Arrastre un destino ODBC a la superficie de diseño, conecte la salida de origen con el destino ODBC y configure el destino para cargar los datos en la tabla DB2 con los datos que extraiga de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use el administrador de conexiones ODBC que creó anteriormente.  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>La copia masiva de datos de tablas de base de datos que admiten ODBC a alguna tabla de SQL Server  
 Puede usar los componentes para copiar los datos de forma masiva de una o varias tablas de base de datos que admiten ODBC a una sola tabla de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 En el ejemplo siguiente se muestra cómo crear una tarea Flujo de datos SSIS que extrae los datos de una tabla de base de datos de Sybase y los carga en una tabla de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Cree un proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   Cree un administrador de conexiones ODBC que use un controlador Sybase ODBC instalado localmente con un DSN que señala a una base de datos de Sybase. De esta base de datos se extraen los datos.  
  
-   Cree un administrador de conexiones OLE DB que se conecte a la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde desee cargar los datos.  
  
-   Arrastre un origen ODBC a la superficie de diseño, después configure el origen para obtener los datos de la tabla de Sybase con los datos que va a copiar. Use el administrador de conexiones ODBC que creó anteriormente.  
  
-   Arrastre un destino OLE DB a la superficie de diseño, conecte la salida de origen con el destino OLE DB y configure el destino para cargar los datos en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con los datos que extraiga de la base de datos de Sybase. Use el administrador de conexiones OLE DB que creó anteriormente.  
  
## <a name="supported-data-types"></a>Tipos de datos admitidos  
 Los componentes de SSIS masivo ODBC admiten todos los tipos de datos ODBC integrados, incluida la compatibilidad con objetos grandes (CLOB y BLOB).  
  
No hay compatibilidad con los tipos de datos de C extensibles, como se describe en las especificaciones de ODBC 3.8. En la tabla siguiente se describe qué tipos de datos de SSIS se usan para cada tipo SQL de ODBC. Un desarrollador de SSIS puede invalidar la asignación predeterminada y especificar un tipo de datos de SSIS para las columnas de entrada/salida sin afectar al rendimiento de las conversiones de datos necesarias.  
  
|Tipo SQL ODBC|Tipo de datos de SSIS|Comentarios|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|Los tipos de datos SQL se asignan a los tipos sin signo de SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) cuando el controlador ODBC establece el UNSIGNED_ATTRIBUTE en SQL_TRUE para ese tipo de datos SQL.|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|Los tipos de datos SQL se asignan a los tipos sin signo de SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) cuando el controlador ODBC establece el UNSIGNED_ATTRIBUTE en SQL_TRUE para ese tipo de datos SQL.|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|Los tipos de datos SQL se asignan a los tipos sin signo de SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) cuando el controlador ODBC establece el UNSIGNED_ATTRIBUTE en SQL_TRUE para ese tipo de datos SQL.|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|Los tipos de datos SQL se asignan a los tipos sin signo de SSIS (DT_UI1, DT_UI2, DT_UI4, DT_UI8) cuando el controlador ODBC establece el UNSIGNED_ATTRIBUTE en SQL_TRUE para ese tipo de datos SQL.|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)|El tipo de datos numérico se asigna a DT_NUMERIC cuando P es mayor o igual que 38 y S es mayor o igual que 0 y S menor o igual que P.|  
||DT_R8|El tipo de datos numérico se asigna a DT_R8 cuando se cumple al menos una de las siguientes condiciones:<br /><br />La precisión es mayor que 38.<br /><br />La escala es menor que cero<br /><br />La escala es mayor que 38<br /><br />La escala es mayor que la precisión|  
||DT_CY|El tipo de datos numérico se asigna a DT_CY cuando se declara como un tipo de datos money.|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)|El tipo de datos decimal se asigna a DT_NUMERIC cuando P es mayor o igual que 38 y S es mayor o igual que 0 y S menor o igual que P.|  
||DT_R8|El tipo de datos decimal se asigna a DT_R8 cuando se cumple al menos una de las siguientes condiciones:<br /><br />La precisión es mayor que 38.<br /><br />La escala es menor que cero<br /><br />La escala es mayor que 38<br /><br />La escala es mayor que la precisión|  
||DT_CY|El tipo de datos decimal se asigna a DT_CY cuando se declara como un tipo de datos money.|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|Los tipos de datos SQL_TIMESTAMP se asignan a DT_DBTIMESTAMP2 si la escala es mayor que 3. En los demás casos, se asignan a DT_DBTIMESTAMP.|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|Se usa DT_STR si la longitud de la columna es menor o igual que 8000 y la propiedad **ExposeStringsAsUnicode** es false.<br /><br />Se usa DT_WSTR si la longitud de la columna es menor o igual que 8000 y la propiedad **ExposeStringsAsUnicode** es true.<br /><br />DT_TEXT se usa si la longitud de la columna es mayor que 8000 y la propiedad **ExposeStringsAsUnicode** es false.<br /><br />DT_NTEXT se usa si la longitud de la columna es mayor que 8000 y la propiedad **ExposeStringsAsUnicode** es true.|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|Se usa DT_NTEXT si la propiedad **ExposeStringsAsUnicode** es true.|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|Se utiliza DT_WSTR si la longitud de la columna es menor o igual que 4000.<br /><br />Se utiliza DT_NTEXT si la longitud de la columna es mayor que 4000.|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|Se utiliza DT_BYTES si la longitud de la columna es menor o igual que 8000.<br /><br />DT_IMAGE si la longitud de la columna es mayor que 8000.|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|Tipos de datos específicos del proveedor|DT_BYTES<br /><br />DT_IMAGE|Se utiliza DT_BYTES si la longitud de la columna es menor o igual que 8000.<br /><br />Se utiliza DT_IMAGE si la longitud de la columna es cero o mayor que 8000.|  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Origen ODBC](../../integration-services/data-flow/odbc-source.md)  
  
-   [Destino ODBC](../../integration-services/data-flow/odbc-destination.md)  
  
 
