---
title: Se han detectado extensiones personalizadas en el servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 86c0aa75e73c59980e8de6456556087201d949d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153105"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>Se han detectado extensiones personalizadas en el servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado valores de extensiones personalizadas en los archivos de configuración, lo que significa que la instalación incluye una o más extensiones personalizadas para el procesamiento, la entrega, la representación, la seguridad o la autenticación de datos. La actualización moverá la configuración de la extensión con el servidor de informes actualizado. Sin embargo, si las extensiones personalizadas se instalan en la carpeta de instalación de servidor de informes existente, los archivos de ensamblado para esas extensiones personalizadas no se moverán a la nueva carpeta de instalación durante el proceso de actualización. Una vez completada la actualización, debe mover los archivos de ensamblado a la nueva carpeta de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Proporciona una arquitectura extensible que permite a los desarrolladores crear extensiones personalizadas para el procesamiento de datos, entrega, representación, seguridad y autenticación.  
  
 Si se utilizan extensiones personalizadas o ensamblados en la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede utilizar la instalación para realizar una actualización, pero es posible que necesite mover las extensiones a la nueva ubicación de instalación una vez que se complete la actualización, o que necesite realizar algún paso antes de la actualización.  
  
> [!NOTE]  
>  El Asesor de actualizaciones no detecta si se configuran ensamblados de código personalizados para su uso en informes para calcular valores de elemento, estilos y formato. Para obtener más información, consulte [otros Reporting Services problemas de actualización](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md).  
  
 Si compró las extensiones personalizadas de un fabricante de software, póngase en contacto con el proveedor para obtener información adicional sobre cómo actualizar la funcionalidad personalizada.  
  
## <a name="corrective-action"></a>Acción correctora  
 Utilice las secciones siguientes para determinar los pasos para realizar además de o antes de realizar una actualización de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 [Procesamiento de datos personalizada o extensiones de entrega](#dataprocdeliver)  
  
 [Extensiones de representación personalizadas](#render)  
  
 [Extensiones de seguridad o de autenticación personalizadas en un servidor de informes de SQL Server 2000](#secauth2000)  
  
 [Extensiones de seguridad o de autenticación personalizadas en un servidor de informes de SQL Server 2005](#secauth2005)  
  
 Una vez completada la actualización, mueva los ensamblados de extensión a la nueva carpeta de instalación y, a continuación, compruebe que las extensiones personalizadas funcionan según lo esperado. Si la extensión no funciona, es posible que deba compilarla:  
  
#### <a name="to-recompile-an-extension"></a>Para volver a compilar una extensión  
  
1.  Copie el archivo Microsoft.ReportingServices.Interfaces.dll en la carpeta que contiene su código fuente.  
  
2.  Abra el proyecto que contiene sus archivos de código fuente y agregue una referencia al archivo Microsoft.ReportingServices.Interfaces.dll.  
  
3.  Vuelva a generar la solución para enlazar la extensión.  
  
 Si decide no continuar con la actualización, quizá decida migrar a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en su lugar. Para obtener información sobre migrar extensiones personalizadas, vea [migrar extensiones personalizadas](#migrcustext) en este tema.  
  
###  <a name="dataprocdeliver"></a> Procesamiento de datos personalizada o extensiones de entrega  
 Si el Asesor de actualizaciones detecta procesamiento de datos personalizado o extensiones de entrega personalizadas, el proceso de actualización no se bloqueará. No obstante, después de completar la actualización, quizá necesite completar pasos adicionales antes de que la funcionalidad personalizada que proporcionan estas extensiones esté operativa. Por ejemplo, debe completar pasos adicionales cuando los archivos de la extensión personalizada estén instalados en la carpeta de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>Pasos de tras la actualización para procesamiento de datos personalizado o extensiones de entrega personalizadas  
  
1.  Mueva los archivos de extensión a la nueva carpeta de programas para el servidor de informes. De forma predeterminada, la carpeta de programa del servidor de informes está en \Program Files\Microsoft SQL Server\MSRS10_50. \< *instance_name*> \report server.  
  
 Para obtener más información, vea "Implementar una extensión de procesamiento de datos" e "Implementar una extensión de entrega" en Libros en pantalla de SQL Server.  
  
###  <a name="render"></a> Extensiones de representación personalizadas  
 Si el Asesor de actualizaciones detecta extensiones de representación personalizadas, el proceso de actualización se bloquea. Puede continuar con el proceso de actualización quitando las entradas de configuración de extensión personalizadas del archivo de configuración. Sin embargo, esto hará que las extensiones personalizadas no estén disponible para los usuarios una vez completada la actualización. Si necesita extensiones de representación personalizadas después de la actualización, debe generar extensiones de representación actualizadas u obtener extensiones de representación actualizadas de un proveedor de extensiones personalizadas.  
  
 Debe hacer lo necesario para habilitar una actualización o, en su lugar, migrar a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!IMPORTANT]  
>  No actualice ni migre el servidor de informes hasta que haya probado y comprobado que la extensión de representación actualizada funciona según lo esperado.  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>Para actualizar extensiones de representación personalizadas  
  
1.  Obtenga las extensiones de representación con las interfaces más recientes.  
  
2.  Quite las entradas de extensión de representación personalizadas antiguas de RSReportServer.config.  
  
3.  Actualice el servidor de informes.  
  
4.  Una vez completada la actualización, instale las extensiones actualizadas en el servidor de informes.  
  
 Para obtener más información, vea "Implementar una extensión de representación" en los Libros en pantalla de SQL Server.  
  
###  <a name="secauth2000"></a> Extensiones de seguridad o de autenticación personalizadas en un servidor de informes de SQL Server 2000  
 Si el Asesor de actualizaciones detecta seguridad o extensiones de autenticación personalizadas en un servidor de informes [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], el proceso de actualización se bloquea. Debe hacer lo necesario para habilitar una actualización o, en su lugar, migrar a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. En cualquier caso, debe actualizar y volver a compilar las extensiones con las interfaces más recientes de Microsoft.ReportingServices.Interfaces.dll, porque las interfaces han cambiado entre [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
> [!IMPORTANT]  
>  No actualice ni migre el servidor de informes hasta que haya probado y comprobado que la extensión de seguridad o autenticación actualizada funciona según lo esperado.  
  
 Si está utilizando una extensión de autenticación personalizada que creó para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe modificar el código fuente para admitir las nuevas clases y miembros introducidos para los informes controlados por modelos.  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>Para actualizar las extensiones de seguridad o de autenticación personalizadas desde un servidor de informes de SQL Server 2000  
  
1.  Actualice y vuelva a compilar cualquier extensión de seguridad o autenticación con las interfaces más recientes.  
  
2.  Quite las entradas de la extensión de seguridad o autenticación de RSReportServer.config.  
  
3.  Actualice el servidor de informes.  
  
4.  Una vez completada la actualización, instale las extensiones actualizadas en el servidor de informes.  
  
 Para obtener más información, vea "Implementar una extensión de seguridad" en los Libros en pantalla de SQL Server.  
  
###  <a name="secauth2005"></a> Extensiones de seguridad o de autenticación personalizadas en un servidor de informes de SQL Server 2005  
 Si el Asesor de actualizaciones detecta seguridad o extensiones de autenticación personalizadas en un servidor de informes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], el proceso de actualización se bloquea. Debe hacer lo necesario para habilitar una actualización o, en su lugar, migrar a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>Para actualizar seguridad o extensiones de autenticación personalizadas de un servidor de informes de SQL Server 2005  
  
1.  Quite las entradas de configuración de la extensión de seguridad o autenticación de RSReportServer.config.  
  
2.  Actualice el servidor de informes.  
  
3.  Una vez completada la actualización, vuelva a agregar las entradas de configuración a RSReportServer.config.  
  
4.  Si los ensamblados de extensión se instalaron en la carpeta de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anterior, muévalas a la nueva carpeta de instalación.  
  
 Para obtener más información, vea "Implementar una extensión de seguridad" en los Libros en pantalla de SQL Server.  
  
###  <a name="migrcustext"></a> Migrar extensiones personalizadas  
 Si decide migrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en lugar de realizar una actualización, utilice los pasos para migrar extensiones personalizadas a la nueva instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>Para migrar extensiones personalizadas a una nueva instancia de Reporting Services  
  
1.  Compile u obtenga las extensiones actualizadas con las interfaces de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] más recientes.  
  
2.  Migre el servidor de informes a una nueva instancia.  
  
3.  Configure las extensiones en la nueva instancia.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
