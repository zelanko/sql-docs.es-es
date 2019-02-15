---
title: Iniciar el generador de informes (generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 506a989494d3f69b5ca9873cc191487bb3b0b296
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290043"
---
# <a name="start-report-builder-report-builder"></a>Iniciar el Generador de informes (Generador de informes)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] incluye independiente y [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] versiones del generador de informes. La versión [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] se puede usar con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo nativo o en modo integrado de SharePoint.  
  
> [!NOTE]  
>  El Generador de informes no se puede instalar en los equipos basados en Itanium 64. Esto se aplica a las versiones independiente y [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] del Generador de informes.  
  
 Si el [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] versión del generador de informes que se abre es una versión anterior del generador de informes, póngase en contacto con su administrador para que se puede actualizar el Administrador de informes y el sitio de SharePoint para usar el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión del generador de informes  
  
 También puede utilizar la versión [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] del Generador de informes para crear los informes en un libro de [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] publicado en SharePoint. Para obtener más información acerca de cómo utilizar el generador de informes con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], consulte [crear un informe de Reporting Services con datos PowerPivot](https://go.microsoft.com/fwlink/?LinkId=185238) en technet.microsoft.com.  
  
 Para iniciar el generador de informes independiente desde el **iniciar** menú en el equipo local o un administrador debe instalar el generador de informes directamente en el equipo antes de la herramienta está disponible para su uso. No se instala la versión independiente al instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]; debe descargarla e instalarla por separado. Para descargar el generador de informes, consulte [generador de informes de Microsoft® SQL Server® 2012](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>Para iniciar el Generador de informes ClickOnce desde el Administrador de informes  
  
1.  En el explorador web, escriba la dirección URL del servidor de informes en la barra de direcciones. De forma predeterminada, la dirección URL es http://\<*nombreDeServidor*>/reports. Se abre el Administrador de informes.  
  
2.  Haga clic en **Generador de informes**.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>Para iniciar el Generador de informes ClickOnce mediante una dirección URL  
  
1.  En el explorador web, escriba la siguiente dirección URL en la barra de direcciones:  
  
     http://\<servername > /reportserver/reportbuilder/ReportBuilder_3_0_0_0.application  
  
2.  Presione ENTRAR.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>Iniciar el Generador de informes ClickOnce en el modo integrado de SharePoint  
  
1.  Navegue al sitio de SharePoint que contenga la biblioteca que desee.  
  
2.  Abra la biblioteca.  
  
3.  Haga clic en **Documentos**.  
  
4.  En el menú **Nuevo documento** , haga clic en **Informe del Generador de informes**.  
  
     El Generador de informes se abre y puede crear un informe o abrirlo en el servidor de informes.  
  
     **Tenga en cuenta** si el **nuevo documento** menú no enumera el **del generador de informes**, **modelo del generador de informes**, y **deorigendedatosdeinforme** opciones, sus tipos de contenido deben agregarse a la biblioteca de SharePoint. Para obtener más información, consulte [Agregar informe Server tipos de contenido en una biblioteca &#40;Reporting Services en modo integrado de SharePoint&#41; ](../add-reporting-services-content-types-to-a-sharepoint-library.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [libros](https://go.microsoft.com/fwlink/?LinkId=154888) en MSDN.Microsoft.com.  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>Iniciar el Generador de informes independiente desde el menú Inicio  
  
1.  En el menú Inicio, haga clic en **todos los programas**y, a continuación, haga clic en [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] **Report Builder**.  
  
2.  Haga clic en **Generador de informes** .  
  
     Se abrirá el Generador de informes y podrá crear o abrir un informe.  
  
3.  Para crear un informe nuevo, haga clic en el icono SQL Server en la esquina superior izquierda del Generador de informes y, entonces, haga clic en Nuevo.  
  
4.  Para abrir un informe almacenado en la máquina local o en un servidor de informes, haga clic en el icono SQL Server de la esquina superior izquierda y, seguidamente, haga clic en Abrir.  
  
     Si no ve el servidor de informes en la lista de servidores existentes, cierre el **abrir informe** cuadro de diálogo y, a continuación, haga clic en **Connect** en la parte inferior del generador de informes para conectarse al servidor.  
  
## <a name="see-also"></a>Vea también  
 [Generador de informes en SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
