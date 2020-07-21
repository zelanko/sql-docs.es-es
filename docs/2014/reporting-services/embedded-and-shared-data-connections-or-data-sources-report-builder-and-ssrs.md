---
title: Conexiones de datos u orígenes de datos incrustados y compartidos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b987dd46f6a60a0d0cadc95cf187566eafa4f527
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109272"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>Conexiones de datos u orígenes de datos incrustados y compartidos (Generador de informes y SSRS)
  Los informes usan las conexiones de datos para recuperar datos para un informe cuando se ejecuta una consulta o cuando se procesa el informe. Puede elegir en una lista de tipos de conexión de datos incrustadas para conectarse a una base de datos relacional, una base de datos multidimensional, un servicio web u otro tipo de origen de datos. Los siguientes términos se usan para describir las conexiones de datos.  
  
-   **Conexión de datos.** También conocido como *origen de datos*. Una conexión de datos consta de un nombre y propiedades de conexión, que dependen del tipo de conexión. Por cuestiones de diseño, una conexión de datos no incluye credenciales. Una conexión de datos no especifica qué datos deben recuperarse del origen de datos externo. Para ello, se especifica una consulta cuando se crea un conjunto de datos.  
  
-   **Definición de origen de datos compartido** .   Un archivo que contiene la representación XML de un origen de datos de informe. Cuando se publica un informe, sus orígenes de datos se guardan en el servidor de informes o sitio de SharePoint como definiciones de origen de datos, independientemente de la definición de informe. Por ejemplo, un administrador del servidor de informes podría actualizar la cadena de conexión o credenciales. En un servidor de informes nativo, el tipo de archivo es .rds. En un sitio de SharePoint, el tipo de archivo es .rsds.  
  
-   **Cadena de conexión.** .   Una cadena de conexión es una versión de cadena de las propiedades de conexión necesarias para conectarse a un origen de datos. Las propiedades de conexión son distintas según el tipo de conexión de datos. Para obtener ejemplos, vea [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
-   **Origen de datos compartido.** Es un origen de datos que está disponible en un servidor de informes o sitio de SharePoint que se va a usar en varios informes.  
  
-   **Origen de datos incrustado.** También conocido como *origen de datos específicos del informe*. Es un origen de datos que se define en un informe y se usa solo en ese informe.  
  
-   **Sus.** Las credenciales son la información de autenticación que se debe proporcionar para poder tener acceso a datos externos.  
  
 La diferencia entre los orígenes de datos incrustados y compartidos es la manera en que se crean, almacenan y administran.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>Orígenes de datos compartidos  
 Los orígenes de datos compartidos resultan útiles cuando se poseen orígenes de datos de uso frecuente. Se recomienda que utilice los orígenes de datos compartidos tanto como sea posible. Facilitan la administración de los informes y del acceso a ellos, y ayudan a mantener una mayor seguridad en el acceso a los informes y los orígenes de datos. Si necesita un origen de datos compartido, pida a su administrador del sistema que le cree uno.  
  
 En el Generador de informes, no puede crear un origen de datos compartido. Puede ir a un origen de datos compartido y seleccionarlo en el servidor de informes. Para obtener más información, consulte [Conexiones de datos, orígenes de datos y cadenas de conexión](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 En el Diseñador de informes, no puede ir a un origen de datos compartido que esté en el servidor de informes. Puede crear orígenes de datos compartidos como parte de un proyecto en el Explorador de soluciones y decidir si se han de implementar en un servidor de informes. Puede decidir usarlos solo de forma local como consecuencia de las diferencias de las credenciales necesarias del equipo o del servidor de informes. Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 El siguiente icono indica un elemento de origen de datos compartido en la jerarquía de carpetas del servidor de informes: ![icono de origen de datos compartido](media/hlp-16datasource.png "Icono de origen de datos compartido")  
  
## <a name="embedded-data-sources"></a>Orígenes de datos incrustados  
 Un origen de datos incrustado es una conexión de datos que se guarda en la definición de informe. La información de conexión a orígenes de datos insertados solo puede utilizarla el informe en el que se incrusta la información. Para definir y administrar los orígenes de datos insertados, utilice el cuadro de diálogo **Propiedades del origen de datos** .  
  
##  <a name="comparing-embedded-and-shared-data-sources"></a><a name="Comparing"></a>Comparar orígenes de datos incrustados y compartidos  
 En la tabla siguiente se resumen las diferencias entre los orígenes de datos compartidos y los incrustados:  
  
|Descripción|Insertado<br /><br /> Origen de datos|Shared<br /><br /> Origen de datos|  
|-----------------|------------------------------|----------------------------|  
|La conexión de datos se incrusta en la definición de informe.|![Disponible](media/greencheck.gif "Disponible")||  
|El puntero a la conexión de datos en el servidor de informes se incrusta en la definición de informe.||![Disponible](media/greencheck.gif "Disponible")|  
|Se administra en el servidor de informes|![Disponible](media/greencheck.gif "Disponible")|![Disponible](media/greencheck.gif "Disponible")|  
|Se requiere para los conjuntos de datos compartidos||![Disponible](media/greencheck.gif "Disponible")|  
|Se requiere para los componentes||![Disponible](media/greencheck.gif "Disponible")|  
  
## <a name="data-source-credentials"></a>Credenciales de origen de datos  
 Las credenciales se usan para crear un origen de datos incrustado, para ejecutar una consulta o para recuperar datos durante el procesamiento del informe. El propietario del origen de datos determina el tipo de credenciales que se deben utilizar para tener acceso a los datos. Las credenciales se administran independientemente de la conexión de datos en un servidor de informes, un sitio de SharePoint o en equipo local en un entorno de creación de informes. Dependiendo del tipo de origen de datos, las credenciales se pueden guardar de forma que no se soliciten o establecerse para solicitarlas a cada usuario. Las credenciales necesarias pueden ser distintas si se va a conectar al origen de datos desde el equipo o desde el servidor de informes. Para obtener más información, vea [especificar credenciales en generador de informes](../../2014/reporting-services/specify-credentials-in-report-builder.md) y [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
## <a name="see-also"></a>Consulte también  
 [Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Conceptos de creación de informes &#40;Generador de informes y SSRS&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos &#40;Generador de informes y SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
