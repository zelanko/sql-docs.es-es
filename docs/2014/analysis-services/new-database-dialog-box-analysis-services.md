---
title: Cuadro de diálogo nueva base de datos (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.newdatabase.f1
ms.assetid: ddc7804b-acb0-4ae4-a88f-e8cdf704c341
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bef5adba44a5202e3cc0fc7f2eb48fae08a0e3c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165715"
---
# <a name="new-database-dialog-box-analysis-services"></a>Nueva base de datos (cuadro de diálogo, Analysis Services)
  Use el cuadro de diálogo **Nueva base de datos** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para crear una nueva base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] vacía. Para mostrar el cuadro de diálogo **Nueva base de datos**, haga clic con el botón derecho en la carpeta **Bases de datos** de una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en **Explorador de objetos** y seleccione **Nueva base de datos**.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Nombre de la base de datos**|Escriba el nombre de la nueva base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Utilizar un nombre de usuario y una contraseña específicos**|Seleccione esta opción para que la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilice las credenciales de seguridad de una cuenta de usuario especificada. Las credenciales especificadas se usarán para el procesamiento, las consultas ROLAP, los enlaces fuera de línea, los cubos locales, los modelos de minería de datos, las particiones remotas, los objetos vinculados y la sincronización del destino al origen. Sin embargo, en el caso las instrucciones DMX OPENQUERY, se usarán las credenciales del usuario actual.|  
|**Nombre de usuario.**|Escriba el dominio y el nombre de la cuenta de usuario que deberá utilizar la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionada. Utilice el siguiente formato:<br /><br /> *\<Nombre de dominio >* **\\**  *\<nombre de la cuenta de usuario >*<br /><br /> Nota: Esta opción está habilitada solo si se ha seleccionado **Usar un nombre de usuario y contraseña específicos** .|  
|**Contraseña**|Escriba la contraseña de la cuenta de usuario especificada en **Nombre de usuario**.|  
|**Utilizar cuenta de servicio**|Seleccione esta opción para que la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilice las credenciales de seguridad asociadas al servicio de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra la base de datos. Las credenciales de la cuenta de servicio se usarán para el procesamiento, las consultas ROLAP, las particiones remotas, los objetos vinculados y la sincronización del destino al origen. Para las instrucciones DMX OPENQUERY, los cubos locales y los modelos de minería de datos, se usarán las credenciales del usuario actual. No se admite esta opción para los enlaces fuera de línea.|  
|**Utilizar las credenciales del usuario actual**|Seleccione esta opción para que la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use las credenciales de seguridad del usuario actual para los enlaces fuera de línea, las instrucciones DMX OPENQUERY, los cubos locales y los modelos de minería de datos. Esta opción no se admite para el procesamiento, las consultas ROLAP, las particiones remotas, los objetos vinculados y la sincronización del destino al origen.|  
|**Default**|Seleccione esta opción para usar las credenciales de la cuenta de usuario predeterminada para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Esta opción usa la configuración predeterminada de la base de datos para el procesamiento de objetos, la sincronización de servidores y la ejecución de instrucciones de minería de datos **Open Query** . Para más información sobre cómo especificar la configuración predeterminada en el nivel de base de datos, vea [Establecer propiedades de bases de datos multidimensionales &#40;Analysis Services&#41;](multidimensional-models/set-multidimensional-database-properties-analysis-services.md).<br /><br /> De forma predeterminada el `DataSourceImpersonationInfo` propiedad de base de datos está establecida en **usar la cuenta de servicio**. Independientemente del valor de propiedad `DataSourceImpersonationInfo`, se usarán las credenciales de usuario actual para los enlaces fuera de línea, las consultas ROLAP, los cubos locales y los modelos de minería de datos.|  
|**Descripción**|Escriba la descripción de la nueva base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Bases de datos modelo multidimensionales &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
