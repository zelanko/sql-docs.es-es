---
title: Recuperar datos de un modelo de minería de datos (DMX) (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b1f3197adf10bfe47a623d83471a0c06004df256
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43265087"
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>Recuperar datos de un modelo de minería de datos (DMX) (SSRS)
  Para usar los datos de un modelo de minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el informe, debe definir un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y uno o más conjuntos de datos de informe. Al crear la definición de origen de datos, debe especificar una cadena de conexión y unas credenciales para poder tener acceso al origen de datos desde el equipo cliente.  
  
 Puede crear una definición de origen de datos incrustada para su uso en un solo informe o una definición de origen de datos compartida que se pueda usar en varios informes. Los procedimientos de este tema explican cómo crear un origen de datos incrustado. Para más información sobre los orígenes de datos compartidos, vea [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56) y [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Después de crear un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede crear uno o más conjuntos de datos. Para cada conjunto de datos, use un diseñador de consultas de predicción de minería de datos (DMX) para crear una consulta DMX que especifique la colección de campos. Para más información, consulte [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
 Después de crear un conjunto de datos, el nombre de éste aparece en el panel Datos de informe como un nodo bajo su origen de datos.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>Para crear un origen de datos de Microsoft SQL Server Analysis Services incrustado  
  
1.  En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo**y, a continuación, haga clic en **Origen de datos**.  
  
2.  En el cuadro de diálogo **Propiedades del origen de datos** , escriba un nombre en el cuadro de texto **Nombre** o acepte el nombre predeterminado.  
  
3.  Compruebe que la opción **Conexión incrustada** está seleccionada.  
  
4.  En la lista desplegable **Tipo** , seleccione **Microsoft SQL Server Analysis Services**.  
  
5.  Especifique una cadena de conexión que funcione con el origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el siguiente ejemplo de cadena de conexión, se especifica la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] en el cliente local.  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  Haga clic en **Credenciales**.  
  
     Establezca las credenciales que se deben usar para conectar con el origen de datos. Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
    > [!NOTE]  
    >  Para probar la conexión del origen de datos, haga clic en **Editar**. En el cuadro de diálogo **Propiedades de conexión** , haga clic en **Probar conexión**. Si la prueba es correcta, aparecerá un mensaje de información que indica que se estableció correctamente la conexión de prueba. Si la prueba no es correcta, aparecerá un mensaje de advertencia con más información acerca de las razones por las que la prueba no se ha realizado correctamente.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     El origen de datos aparece en el panel Datos de informe.  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>Crear un conjunto de datos de Microsoft SQL Server Analysis Services  
  
1.  En el panel **Datos de informe** , haga clic con el botón derecho en el nombre del origen de datos que se conecta a un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, después, haga clic en **Agregar conjunto de datos**.  
  
2.  En el cuadro de diálogo **Propiedades del conjunto de datos** , escriba un nombre en el cuadro de texto **Nombre** .  
  
3.  En el cuadro **Origen de datos**, compruebe que el nombre es el nombre de un origen de datos que se conecta con un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
4.  Haga clic en **Diseñador de consultas** para abrir el diseñador gráfico de consultas y generar interactivamente una consulta. Si el diseñador de consultas se abre en modo MDX, haga clic en **Tipo de comando DMX** (![Cambiar a la vista del lenguaje de consultas DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Cambiar a la vista del lenguaje de consultas DMX")) en la barra de herramientas para cambiar al diseñador de consultas de minería de datos. Para más información, consulte [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
     O bien, para importar una consulta DMX existente desde otro informe, haga clic en **Importar**y, a continuación, navegue hasta el archivo .rdl que contiene la consulta DMX. No se admite la importación de una consulta desde un archivo .dmx.  
  
5.  Después de crear y ejecutar la consulta para ver los resultados del ejemplo, haga clic en **Aceptar**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     El conjunto de datos y su colección de campos aparecen en el panel Datos de informe bajo el nodo del origen de datos.  
  
## <a name="see-also"></a>Ver también  
 [Tipo de conexión de Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
