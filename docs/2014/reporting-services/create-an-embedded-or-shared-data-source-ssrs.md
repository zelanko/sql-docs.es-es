---
title: Crear un origen de datos incrustado o compartido (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: d9da0718a6eee5fda00d6418a5b6a624f8380c7d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033486"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>Crear un origen de datos incrustado o compartido (SSRS)
  Un origen de datos de informe especifica la información de nombre y cadena de conexión. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite dos tipos de orígenes de datos: incrustados y compartidos. Un origen de datos incrustado se define en una definición de informe y se usa solamente en ese informe. Un origen de datos compartido se define como un elemento independiente y se puede usar en varios informes. Para obtener más información, consulte [incrustados y compartidos conexiones de datos u orígenes de datos &#40;generador de informes y SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 En el Generador de informes, puede desplazarse al servidor de informes o al sitio de SharePoint y seleccionar orígenes de datos o crear orígenes de datos incrustados. No puede crear orígenes de datos compartidos en el Generador de informes.  
  
 En el Diseñador de informes, puede crear orígenes de datos compartidos o incrustados. En el panel datos de informe, comience a crear una referencia de origen de datos y, a continuación, seleccione el **New** opción. Después de crear la referencia de origen de datos, se agregará automáticamente un nuevo origen de datos compartido al Explorador de soluciones en la carpeta de orígenes de datos compartidos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 También puede crear orígenes de datos compartidos directamente en un servidor de informes o un sitio de SharePoint. Para obtener más información, consulte [crear, eliminar o modificar un origen de datos compartido &#40;el Administrador de informes&#41; ](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) o [crear y administrar orígenes de datos compartidos &#40;Reporting Services en modo integrado de SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>Para crear un origen de datos incrustado o compartido  
  
1.  En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo** y, a continuación, haga clic en **Origen de datos**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
    > [!NOTE]  
    >  Si el panel Datos de informe no es visible, haga clic en **Datos de informe** en el menú **Ver** .  
  
2.  En el cuadro de texto **Nombre** , escriba un nombre para el origen de datos o acepte el valor predeterminado. El nombre del origen de datos se utiliza internamente en el informe. Para evitar confusiones, se recomienda que el nombre del origen de datos contenga el nombre de la base de datos especificada en la cadena de conexión.  
  
3.  Para un origen de datos incrustado, compruebe que **conexión incrustada** está seleccionada.  
  
    1.  En la lista desplegable **Tipo** , seleccione un tipo de origen de datos (por ejemplo, **Microsoft SQL Server** u **OLE DB**).  
  
    2.  Especifique una cadena de conexión usando una de las alternativas siguientes:  
  
    -   Escriba la cadena de conexión directamente en el cuadro de texto **Cadena de conexión** . Para obtener una lista de cadenas de conexión de ejemplo, vea [conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md) o [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   Haga clic en el botón de expresión (**fx** ) para crear una expresión que dé como resultado una cadena de conexión. En el cuadro de diálogo **Expresión** , escriba la expresión en el panel Expresión. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   Haga clic en **Editar** para abrir el cuadro de diálogo **Propiedades de conexión** para el tipo de origen de datos que eligió en el paso 2.  
  
         Rellene los campos del cuadro de diálogo **Propiedades de conexión** según corresponda para el tipo de origen de datos. Las propiedades de conexión incluyen el tipo de origen de datos, el nombre del origen de datos, y las credenciales que se deben usar. Después de especificar los valores en este cuadro de diálogo, haga clic en **Probar conexión** para comprobar que el origen de datos está disponible y que las credenciales que especificó son correctas. Para más información sobre tipos de orígenes de datos específicos, vea los temas en [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md).  
  
4.  Para un origen de datos compartidos, comprobar que **utilizar referencia de origen de datos compartido** está seleccionada.  
  
    1.  Haga clic en **Nueva**. En el cuadro de diálogo de propiedades **Origen de datos compartido** , siga los pasos 2 y 3 para crear un nuevo origen de datos.  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         El nuevo origen de datos compartido aparece en la carpeta Orígenes de datos compartidos del Explorador de soluciones.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     El origen de datos aparece en el panel Datos de informe. En el panel Datos de informe, un origen de datos compartido señala la definición del origen de datos compartido. En el Generador de informes, la definición del origen de datos está en un servidor de informes o en un sitio de SharePoint. En el Diseñador de informes, la definición del origen de datos es un archivo del Explorador de soluciones en la carpeta de orígenes de datos compartidos.  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>Para importar un origen de datos existente en el Diseñador de informes  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Orígenes de datos compartidos** del proyecto de servidor de informes y, después, haga clic en **Agregar elemento existente**. Se abrirá el cuadro de diálogo **Agregar elemento existente** .  
  
2.  Navegue a un archivo existente de origen de datos compartido de definición de informe (rds) y, después, haga clic en **Abrir**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>Para convertir un origen de datos incrustado en un origen de datos compartido en el Diseñador de informes  
  
-   En el panel datos de informe, haga clic en el origen de datos y, a continuación, haga clic en **convertir a origen de datos compartidos**.  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>Para convertir un origen de datos compartido en un origen de datos incrustado en el Generador de informes  
  
-   En el panel datos de informe, haga clic en el origen de datos y abra **propiedades del origen de datos**.  
  
-   Haga clic en **conexión incrustada** y termine de crear el origen de datos incrustado como se describe en el procedimiento anterior.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de las credenciales en un origen de datos de Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Convertir un origen de datos incrustado en compartido &#40;generador de informes y SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [Enlazar un informe o un modelo con un origen de datos compartido &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Configurar propiedades de origen de datos para un informe &#40;Administrador de informes&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
