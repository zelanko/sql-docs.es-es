---
title: El directorio virtual tiene un método de autenticación no compatible (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 26420df466860677f22d39d57133568a2f02bc68
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952008"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>El directorio virtual tiene un método de autenticación no admitido (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado un método de autenticación no compatible en el directorio virtual del Administrador de informes o del servidor de informes. Entre los métodos de autenticación no admitidos por la actualización se incluyen: Anónimo, Implícito y .NET Passport.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El programa de instalación no puede actualizar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que usa uno de los métodos de autenticación siguientes  
  
-   Anónimas  
  
-   Resumen  
  
-   .NET Passport  
  
 Para continuar, puede modificar el método de autenticación especificado para los directorios virtuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en Internet Information Services (IIS) o puede migrar su instalación. Para obtener más información sobre la migración de una instalación, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Para continuar con la actualización, modifique el método de autenticación en IIS para los directorios virtuales ReportServer y Reports. Para obtener más información sobre cómo modificar los métodos de autenticación en IIS, vea la documentación de IIS. Después de modificar el método de autenticación para los directorios virtuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vuelva a ejecutar el Asesor de actualizaciones para confirmar que no hay problemas de actualización.  
  
## <a name="see-also"></a>Consulte también  
 [Reporting Services problemas de actualización &#40;el asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
