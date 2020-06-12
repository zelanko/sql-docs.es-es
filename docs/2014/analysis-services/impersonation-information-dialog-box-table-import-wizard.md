---
title: Información de suplantación (cuadro de diálogo del Asistente para la importación de tablas) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.impersonationinfo.f1
ms.assetid: bee7eee5-0650-41f1-a372-5076ae97a58c
author: minewiskan
ms.author: owend
ms.openlocfilehash: b29901213da4653c2d8867b9f450b359c39bded3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544259"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>Cuadro de diálogo Información de suplantación (Asistente para la importación de tablas)
  Use la página **Información de suplantación** para especificar las credenciales que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizará para conectarse al origen de datos. Para más información sobre la suplantación de credenciales, vea [Impersonation &#40;SSAS Tabular&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de usuario y contraseña específicos de Windows**  
 Seleccione esta opción para que el modelo tabular utilice las credenciales de seguridad de una cuenta de usuario de Windows determinada.  
  
 **Nombre de usuario**  
 Escriba el dominio y el nombre de la cuenta de usuario que debe usarse. Utilice el siguiente formato:  
  
 *\<Domain name>* **\\** *\<User account name>*  
  
 Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .  
  
 **Contraseña**  
 Escriba la contraseña de la cuenta de usuario que debe usar el objeto del modelo tabular.  
  
 Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .  
  
 **Cuenta de servicio**  
 Seleccione esta opción para usar las credenciales de seguridad asociadas al servicio de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra el modelo.  
  
## <a name="see-also"></a>Consulte también  
 [Suplantación &#40;SSAS tabular&#41;](tabular-models/impersonation-ssas-tabular.md)  
  
  
