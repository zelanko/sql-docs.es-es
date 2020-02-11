---
title: Conexiones de datos, orígenes de datos y cadenas de conexión en Generador de informes | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb8d81c9c47f00ed84036accf86768d084072c4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109488"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a>Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes
  Para incluir datos en un informe, debe crear conexiones de datos y conjuntos de datos. Una conexión de datos contiene información acerca de cómo tener acceso a un origen de datos externo. Un conjunto de datos contiene un comando de consulta que especifique los datos que se van a incluir mediante la conexión de datos.  
  
1.  **Orígenes de datos en el panel datos de informe** Un origen de datos aparece en el panel datos de informe después de crear un origen de datos incrustado o de agregar un origen de datos compartido.  
  
2.  **Cuadro de diálogo conexión** Utilice el cuadro de diálogo conexión para generar una cadena de conexión o para pegar una cadena de conexión.  
  
3.  **Información de conexión de datos** La cadena de conexión se pasa a la extensión de datos.  
  
4.  **Credenciales** de Las credenciales se administran de forma independiente de la cadena de conexión.  
  
5.  **Extensión de datos/proveedor de datos** La conexión a los datos puede realizarse a través de varios niveles de acceso a datos.  
  
6.  **Orígenes de datos externos** Recuperar datos de bases de datos relacionales, bases de datos multidimensionales, listas de SharePoint, servicios web o modelos de informe.  
  
 Para obtener más información, vea conexiones de datos [y orígenes de datos incrustados y Compartidos &#40;generador de informes y SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) y [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Los datos también pueden incluirse en un informe utilizando, orígenes de datos compartidos predefinidos, conjuntos de datos y elementos de informe. Estos elementos ya tienen la información de la conexión de datos que necesita. Para obtener más información, vea [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 ![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
##  <a name="ConnectionString"></a>Ejemplos de cadenas de conexión  
 Una conexión de datos incluye una cadena de conexión que suele proporcionar el propietario del origen de datos externo. En la tabla siguiente, se muestran ejemplos de cadenas de conexión para diferentes tipos de orígenes de datos externos.  
  
|**Origen de datos**|**Ejemplo**|**Descripción**|  
|---------------------|-----------------|---------------------|  
|Base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el servidor local|`data source="(local)";initial catalog=AdventureWorks2012`|Establezca el tipo de origen de datos en `SQL Server`.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]base de datos de instancia|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|Establezca el tipo de origen de datos en `SQL Server`.|  
|Base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|Establezca el tipo de origen de datos en `SQL Server`.|  
|Base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el servidor local|`data source=localhost;initial catalog=Adventure Works DW 2012`|Establezca el tipo de origen de datos en `SQL Server Analysis Services`.|  
|Lista de SharePoint|`data source=http://MySharePointWeb/MySharePointSite/`|Establezca el tipo de origen de datos en `SharePoint List`.|  
||||  
|Modelos de informe|No aplicable.|No necesita una cadena de conexión para un modelo de informe. En el Generador de informes, vaya al servidor de informes y seleccione el archivo .smdl que constituye el modelo de informe.|  
|Servidor Oracle|`data source=myserver`|Configure el tipo de origen de datos en `Oracle`. También es necesario instalar las herramientas de cliente de Oracle tanto en el equipo del Generador de informes como en el servidor de informes.|  
|Origen de datos SAP Netweaver BI|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Configure el tipo de origen de datos en `SAP NetWeaver BI`.|  
|Origen de datos de Hyperion Essbase|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Configure el tipo de origen de datos en `Hyperion Essbase`.|  
|Origen de datos de Teradata|`data source=`* \<NN>. \<Nnn>. \<Nnn>. N \<>*`;`|Configure el tipo de origen de datos en `Teradata`. La cadena de conexión es una dirección IP (protocolo de Internet) formada por cuatro campos, donde cada campo puede tener de uno a tres dígitos.|  
|Origen de datos de Teradata|`Database=`nombre de la base de `; data source=` * \<datos>* * \<NN*N *>.\< NNN>. \<Nnn>. N \<* NN*>*`;Use X Views=False;Restrict to Default Database=True`|Establezca el tipo de origen de datos en `Teradata`, de modo similar a como se hizo en el ejemplo anterior. Usa solamente la base de datos predeterminada que se especifica en la etiqueta de la base de datos, sin detectar automáticamente las relaciones de los datos.|  
|Origen de datos XML, servicio web|`data source=http://adventure-works.com/results.aspx`|Configure el tipo de origen de datos en `XML`. La cadena de conexión es una dirección URL de un servicio web que admite el Lenguaje de definición de servicios web (WSDL).|  
|Origen de datos XML, documento XML|`http://localhost/XML/Customers.xml`|Configure el tipo de origen de datos en `XML`. La cadena de conexión es una dirección URL que lleva al documento XML.|  
|Origen de datos XML, documento XML incrustado|*Vacío*|Configure el tipo de origen de datos en `XML`. Los datos XML se incrustan en la definición de informe.|  
  
 Para obtener más información sobre cada tipo de conexión, vea [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) y [orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  

  
##  <a name="Creating"></a>Crear orígenes de datos  
 Para crear un origen de datos insertados, debe tener una cadena de conexión y las credenciales necesarias para el acceso a los datos. Esta información normalmente procede del propietario del origen de datos. La conexión de datos se guarda en la definición de informe como parte del origen de datos. Las credenciales se administran independientemente de la conexión. Para obtener instrucciones paso a paso, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Algunos tipos de credenciales podrían no ser compatibles con todos los escenarios que el Generador de informes utiliza: ejecutar una consulta en el diseñador de consultas, obtener una vista previa de un informe desde un equipo cuando no se está conectado a un servidor de informes y ejecutar el informe desde el servidor de informes. Le recomendamos que use los orígenes de datos compartidos siempre que sea posible. Puede almacenar las credenciales para un origen de datos compartido en el servidor de informes. Para más información, vea [Especificar credenciales en el Generador de informes](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
 Para crear un origen de datos compartido, debe usar Administrador de informes para crear el origen de datos directamente en el servidor de informes o usar un entorno de creación como Diseñador de informes en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [crear un origen de datos incrustado o compartido &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md).  
  

  
## <a name="see-also"></a>Consulte también  
 [Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Elementos de informe &#40;Generador de informes y SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
