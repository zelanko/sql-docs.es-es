---
title: Base de datos de cuadro de diálogo de propiedades (SSAS - Multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.databaseproperties.f1
ms.assetid: 70f000b7-917f-4699-b142-7a0d13ff767c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be4133aa143ecf0e1fb9b50c40a38a73b4207f30
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082319"
---
# <a name="database-properties-dialog-box-ssas---multidimensional"></a>Propiedades de la base de datos (cuadro de diálogo) (SSAS: multidimensional)
  Use el cuadro de diálogo **Propiedades de la base de datos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para establecer las propiedades de una base de datos en una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para mostrar el cuadro de diálogo **Propiedades de la base de datos** , haga clic con el botón derecho en una base de datos del Explorador de objetos y seleccione **Propiedades**.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Name**|Escriba un nombre para cambiar el nombre de la base de datos.|  
|**ID**|Muestra el identificador de la base de datos.|  
|**Descripción**|Escriba una descripción para cambiar la descripción de la base de datos.|  
|**Marca de tiempo de creación**|Muestra la fecha y hora en que se creó la base de datos.|  
|**Última actualización de esquema**|Muestra la fecha y hora en que se actualizaron por última vez los metadatos de la base de datos.|  
|**Última actualización**|Muestra la fecha y hora en que se actualizaron por última vez los datos de la base de datos.|  
|**Información de suplantación de origen de datos**|Seleccione la información de suplantación que utilizará la base de datos para conectarse a los orígenes de datos contenidos en la base de datos e interactuar con estos. Los valores válidos incluyen los siguientes:<br /><br /> **ImpersonateAccount** (use un nombre de usuario y una contraseña de Windows específicos).<br /><br /> **ImpersonateService** (use la cuenta de servicio).<br /><br /> **ImpersonateCurrentUser** (use las credenciales del usuario actual).<br /><br /> **Default** (use la cuenta de servicio para las operaciones MOLAP y el usuario actual para la minería de datos).<br /><br /> Aunque es posible establecer la configuración de la suplantación del origen de datos en el nivel de base de datos, esto solo afectará a aquellos orígenes de datos que especifiquen **Heredar** en la configuración de suplantación. La configuración de suplantación especificada directamente en el origen de datos invalidará siempre a la configuración especificada en el nivel de base de datos.<br /><br /> Al elegir una opción de suplantación, tenga en cuenta los tipos de operaciones que deberán admitirse. Algunas operaciones, tales como el procesamiento, no pueden realizarse.|  
|**Procesado por última vez**|Muestra la fecha y hora en que se procesó por última vez la base de datos.|  
|**Tamaño estimado**|Muestra el tamaño estimado de la base de datos.|  
|**Ubicación de almacenamiento**|Especifica la ubicación de la base de datos. Si la base de datos se encuentra en el directorio de datos predeterminado, este valor estará vacío.|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Bases de datos de modelos multidimensionales &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
