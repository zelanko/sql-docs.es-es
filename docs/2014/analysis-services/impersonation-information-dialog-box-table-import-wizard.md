---
title: Cuadro de diálogo de información de suplantación (Asistente para importación de tablas) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.impersonationinfo.f1
ms.assetid: bee7eee5-0650-41f1-a372-5076ae97a58c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d271bbfdf31a24304961d71e4501ea7ae4579440
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047566"
---
# <a name="impersonation-information-dialog-box-table-import-wizard"></a>Cuadro de diálogo Información de suplantación (Asistente para la importación de tablas)
  Use la página **Información de suplantación** para especificar las credenciales que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizará para conectarse al origen de datos. Para más información sobre la suplantación de credenciales, vea [Impersonation &#40;SSAS Tabular&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de usuario específico de Windows y contraseña**  
 Seleccione esta opción para que el modelo tabular utilice las credenciales de seguridad de una cuenta de usuario de Windows determinada.  
  
 **Nombre de usuario.**  
 Escriba el dominio y el nombre de la cuenta de usuario que debe usarse. Utilice el siguiente formato:  
  
 *\<Nombre de dominio >* **\\**  *\<nombre de la cuenta de usuario >*  
  
 Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .  
  
 **Contraseña**  
 Escriba la contraseña de la cuenta de usuario que debe usar el objeto del modelo tabular.  
  
 Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .  
  
 **Cuenta de servicio**  
 Seleccione esta opción para usar las credenciales de seguridad asociadas al servicio de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra el modelo.  
  
## <a name="see-also"></a>Vea también  
 [Suplantación &#40;Tabular de SSAS&#41;](tabular-models/impersonation-ssas-tabular.md)  
  
  
