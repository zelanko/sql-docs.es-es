---
title: Directorio virtual tiene un no admitido (Asesor de actualizaciones) del método de autenticación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 992e0f125d80a4735a356a853dab55439149e7ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091056"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>El directorio virtual tiene un método de autenticación no admitido (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado un método de autenticación no compatible en el directorio virtual del Administrador de informes o del servidor de informes. Entre los métodos de autenticación no admitidos por la actualización se incluyen: Anónimo, Implícito y .NET Passport.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El programa de instalación no puede actualizar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que usa uno de los métodos de autenticación siguientes  
  
-   Anónimo  
  
-   Resumen  
  
-   .NET Passport  
  
 Para continuar, puede modificar el método de autenticación especificado para los directorios virtuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en Internet Information Services (IIS) o puede migrar su instalación. Para obtener más información sobre la migración de una instalación, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Para continuar con la actualización, modifique el método de autenticación en IIS para los directorios virtuales ReportServer y Reports. Para obtener más información sobre cómo modificar los métodos de autenticación en IIS, vea la documentación de IIS. Después de modificar el método de autenticación para los directorios virtuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vuelva a ejecutar el Asesor de actualizaciones para confirmar que no hay problemas de actualización.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
