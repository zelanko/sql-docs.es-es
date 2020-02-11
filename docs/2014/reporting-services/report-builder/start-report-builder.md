---
title: Iniciar Generador de informes (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fc123be862320cd35ccf4aec76d8bc9cf7877af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107599"
---
# <a name="start-report-builder-report-builder"></a>Iniciar el Generador de informes (Generador de informes)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]incluye [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] versiones independientes de generador de informes. La versión [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] se puede usar con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo nativo o en modo integrado de SharePoint.  
  
> [!NOTE]  
>  El Generador de informes no se puede instalar en los equipos basados en Itanium 64. Esto se aplica a las versiones independiente y [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] del Generador de informes.  
  
 Si la [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] versión de generador de informes que se abre es una versión anterior de generador de informes, póngase en contacto con el administrador que pueda actualizar administrador de informes y el sitio [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de SharePoint para usar la versión de generador de informes  
  
 También puede utilizar la versión [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] del Generador de informes para crear los informes en un libro de [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] publicado en SharePoint. Para obtener más información sobre el uso [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]de generador de informes con, vea [crear un informe de Reporting Services con datos PowerPivot](https://go.microsoft.com/fwlink/?LinkId=185238) en TechNet.Microsoft.com.  
  
 Para iniciar Generador de informes independiente desde el menú **Inicio** del equipo local, usted o un administrador deben instalar generador de informes directamente en el equipo antes de que la herramienta esté disponible para su uso. No se instala la versión independiente al instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]; debe descargarla e instalarla por separado. Para descargar Generador de informes, consulte [Microsoft® SQL Server® 2012 generador de informes](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>Para iniciar el Generador de informes ClickOnce desde el Administrador de informes  
  
1.  En el explorador web, escriba la dirección URL del servidor de informes en la barra de direcciones. De forma predeterminada, la dirección URL es http://\<*nombreDeServidor*>/reports. Se abre el Administrador de informes.  
  
2.  Haga clic en **Generador de informes**.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>Para iniciar el Generador de informes ClickOnce mediante una dirección URL  
  
1.  En el explorador web, escriba la siguiente dirección URL en la barra de direcciones:  
  
     http://\<ServerName>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0. Application  
  
2.  Presione ENTRAR.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>Iniciar el Generador de informes ClickOnce en el modo integrado de SharePoint  
  
1.  Navegue al sitio de SharePoint que contenga la biblioteca que desee.  
  
2.  Abra la biblioteca.  
  
3.  Haga clic en **Documentos**.  
  
4.  En el menú **Nuevo documento** , haga clic en **Informe del Generador de informes**.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
     **Nota:** Si en el menú **nuevo documento** no se muestran las opciones **Informe de generador de informes**, **modelo de generador de informes**y origen de **datos de informe** , es necesario agregar sus tipos de contenido a la biblioteca de SharePoint. Para obtener más información, vea [agregar tipos de contenido del servidor de informes a una biblioteca &#40;Reporting Services en el modo integrado de SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los [libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=154888) de en MSDN.Microsoft.com.  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>Iniciar el Generador de informes independiente desde el menú Inicio  
  
1.  En el menú Inicio, haga clic en **todos los programas**y [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] , a continuación, haga clic en **generador de informes**.  
  
2.  Haga clic en **Generador de informes** .  
  
     Se abrirá el Generador de informes y podrá crear o abrir un informe.  
  
3.  Para crear un informe nuevo, haga clic en el icono SQL Server en la esquina superior izquierda del Generador de informes y, entonces, haga clic en Nuevo.  
  
4.  Para abrir un informe almacenado en la máquina local o en un servidor de informes, haga clic en el icono SQL Server de la esquina superior izquierda y, seguidamente, haga clic en Abrir.  
  
     Si no ve el servidor de informes en la lista de servidores existentes, cierre el cuadro de diálogo **abrir Informe** y, a continuación, haga clic en **conectar** en la parte inferior de generador de informes para conectarse al servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Generador de informes en SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
