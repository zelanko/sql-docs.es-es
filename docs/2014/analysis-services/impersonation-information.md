---
title: Información de suplantación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 90a9d2102df9bd1b6cdf2bf1e4c7b3386c0fa825
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106011"
---
# <a name="impersonation-information"></a>Información de suplantación
  Use la página **Información de suplantación** para especificar las credenciales que Analysis Services utilizará para conectarse al origen de datos.  
  
## <a name="options"></a>Opciones  
 **Usar un nombre de usuario de Windows específico y una contraseña**  
 Seleccione esta opción si quiere que el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use las credenciales de seguridad de una cuenta de usuario de Windows determinada. Las credenciales especificadas se usarán para el procesamiento, las consultas ROLAP, los enlaces fuera de línea, los cubos locales, los modelos de minería de datos, las particiones remotas, los objetos vinculados y la sincronización del destino al origen. En cambio, en el caso de las instrucciones OPENQUERY de extensiones de minería de datos (DMX), esta opción se omite y se usarán las credenciales del usuario actual.  
  
 **Nombre de usuario.**  
 Escriba el dominio y el nombre de la cuenta de usuario que debe usar el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionado. Utilice el siguiente formato:  
  
 *\<Nombre de dominio >* **\\**  *\<nombre de la cuenta de usuario >*  
  
 Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .  
  
 **Contraseña**  
 Escriba la contraseña de la cuenta de usuario que debe usar el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionado.  
  
 Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .  
  
 **Utilizar cuenta de servicio**  
 Seleccione esta opción para que el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use las credenciales de seguridad asociadas al servicio de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra el objeto. Las credenciales de la cuenta de servicio se usarán para el procesamiento, las consultas ROLAP, las particiones remotas, los objetos vinculados y la sincronización del destino al origen. No obstante, en el caso de las instrucciones OPENQUERY de las extensiones de minería de datos (DMX), los cubos locales y los modelos de minería de datos, se usarán las credenciales del usuario actual. No se admite esta opción para los enlaces fuera de línea.  
  
 **Utilizar las credenciales del usuario actual**  
 Seleccione esta opción para que el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use las credenciales de seguridad del usuario actual para los enlaces fuera de línea, las instrucciones DMX OPENQUERY, los cubos locales y los modelos de minería de datos. Esta opción no se admite para el procesamiento, las consultas ROLAP, las particiones remotas, los objetos vinculados y la sincronización del destino al origen.  
  
 **Heredar**  
 Seleccione esta opción para usar el comportamiento de suplantación, definido en el nivel de la base de datos, que ha establecido por el administrador del servidor mediante la propiedad de base de datos `DataSourceImpersonation`.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos en modelos multidimensionales](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Orígenes de datos admitidos &#40;SSAS Multidimensional&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  