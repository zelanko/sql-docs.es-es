---
title: Recuperar datos de un modelo de minería de datos (DMX) (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7cc94e2945ac50537bd3ee42241909b5dc9c2cef
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107130"
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>Recuperar datos de un modelo de minería de datos (DMX) (SSRS)
  Para usar los datos de un modelo de minería de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en el informe, debe definir un origen de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y uno o más conjuntos de datos de informe. Al crear la definición de origen de datos, debe especificar una cadena de conexión y unas credenciales para poder tener acceso al origen de datos desde el equipo cliente.  
  
 Puede crear una definición de origen de datos incrustada para su uso en un solo informe o una definición de origen de datos compartida que se pueda usar en varios informes. Los procedimientos de este tema explican cómo crear un origen de datos incrustado. Para más información sobre los orígenes de datos compartidos, vea [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) y [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Después de crear un origen de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , puede crear uno o más conjuntos de datos. Para cada conjunto de datos, use un diseñador de consultas de predicción de minería de datos (DMX) para crear una consulta DMX que especifique la colección de campos. Para más información, consulte [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](analysis-services-dmx-query-designer-user-interface.md).  
  
 Después de crear un conjunto de datos, el nombre de éste aparece en el panel Datos de informe como un nodo bajo su origen de datos.  
  
 Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos.  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>Para crear un origen de datos de Microsoft SQL Server Analysis Services incrustado  
  
1.  En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo**y, a continuación, haga clic en **Origen de datos**.  
  
2.  En el cuadro de diálogo **Propiedades del origen de datos** , escriba un nombre en el cuadro de texto **Nombre** o acepte el nombre predeterminado.  
  
3.  Compruebe que la opción **Conexión incrustada** está seleccionada.  
  
4.  En la lista desplegable **Tipo** , seleccione **Microsoft SQL Server Analysis Services**.  
  
5.  Especifique una cadena de conexión que funcione con el origen de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
     Póngase en contacto con el administrador de bases de datos y solicite la información de conexión y las credenciales que debe usar para conectar con el origen de datos. En el siguiente ejemplo de cadena de conexión, se especifica la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] en el cliente local.  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  Haga clic en **Credenciales**.  
  
     Establezca las credenciales que se deben usar para conectar con el origen de datos. Para más información, consulte [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../integration-services/connection-manager/data-sources.md).  
  
    > [!NOTE]  
    >  Para probar la conexión del origen de datos, haga clic en **Editar**. En el cuadro de diálogo **Propiedades de conexión** , haga clic en **Probar conexión**. Si la prueba es correcta, aparecerá un mensaje de información que indica que se estableció correctamente la conexión de prueba. Si la prueba no es correcta, aparecerá un mensaje de advertencia con más información acerca de las razones por las que la prueba no se ha realizado correctamente.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     El origen de datos aparece en el panel Datos de informe.  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>Crear un conjunto de datos de Microsoft SQL Server Analysis Services  
  
1.  En el panel **Datos de informe** , haga clic con el botón derecho en el nombre del origen de datos que se conecta a un origen de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y, después, haga clic en **Agregar conjunto de datos**.  
  
2.  En el cuadro de diálogo **Propiedades del conjunto de datos** , escriba un nombre en el cuadro de texto **Nombre** .  
  
3.  En el cuadro **Origen de datos**, compruebe que el nombre es el nombre de un origen de datos que se conecta con un origen de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
4.  Haga clic en **Diseñador de consultas** para abrir el diseñador gráfico de consultas y generar interactivamente una consulta. Si el diseñador de consultas se abre en modo MDX, haga clic en **Tipo de comando DMX** (![Cambiar a la vista del lenguaje de consultas DMX](../media/rsqdicon-commandtypedmx.gif "Cambiar a la vista del lenguaje de consultas DMX")) en la barra de herramientas para cambiar al diseñador de consultas de minería de datos. Para más información, consulte [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](analysis-services-dmx-query-designer-user-interface.md).  
  
     O bien, para importar una consulta DMX existente desde otro informe, haga clic en **Importar**y, a continuación, navegue hasta el archivo .rdl que contiene la consulta DMX. No se admite la importación de una consulta desde un archivo .dmx.  
  
5.  Después de crear y ejecutar la consulta para ver los resultados del ejemplo, haga clic en **Aceptar**.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     El conjunto de datos y su colección de campos aparecen en el panel Datos de informe bajo el nodo del origen de datos.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de conexión de Analysis Services para DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
