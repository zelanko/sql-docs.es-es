---
title: Programa para la mejora de la experiencia del usuario de SQL Server Data Tools | Microsoft Docs
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
caps.latest.revision: "11"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d3ac32a1bded13f7d2411fac6100353f3ec7e2c9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="customer-experience-improvement-program-for-sql-server-data-tools"></a>Programa para la mejora de la experiencia del usuario de SQL Server Data Tools
  Obtenga información sobre el modo en que el Programa para la mejora de la experiencia del usuario (CEIP) ayuda a Microsoft a identificar formas de mejorar el software.  Puede configurar herramientas para participar o dejar de hacerlo en cualquier momento.  
  
> [!NOTE]  
>  Para ver una explicación de las prácticas de recopilación y uso de datos de usuario de las versiones de Microsoft SQL Server 2016 y de cualquier otro producto y servicio, consulte esta [declaración de privacidad de Microsoft](https://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>Participación en el CEIP de SQL Server Data Tools o cancelación de esta  
 El Programa para la mejora de la experiencia del usuario está concebido para ayudar a Microsoft a mejorar sus productos a lo largo del tiempo. El programa recopila información sobre el hardware del equipo y la forma en que los usuarios usan el producto sin interrumpir las tareas que realizan en el equipo. La información recopilada ayuda a Microsoft a identificar las características que se deben mejorar. En este documento se explica cómo participar en el CEIP de SQL Server Data Tools (SSDT) para Visual Studio 2017, Visual Studio 2015 y Visual Studio 2013. Asimismo, también se incluyen los detalles para dejar de hacerlo.  

### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2017"></a>Elección y control sobre el CEIP y SQL Server Data Tools para Visual Studio 2017  
 SSDT para Visual Studio 2017 es la herramienta de modelado de datos incluida en SQL Server 2017. Usa las opciones del CEIP integradas en Visual Studio 2017. Puede obtener más información sobre cómo enviar comentarios a través del CEIP de Visual Studio 2017 en este [documento de ayuda de Visual Studio](https://www.visualstudio.com/en-us/docs/work/connect/give-feedback).  
  
 En las versiones preliminares de SQL Server 2017, el CEIP está activado de forma predeterminada. Puede desactivarlo o volver a activarlo con las instrucciones siguientes.  
  
 **En Visual Studio (se aplica a las instalaciones de idioma completo de Visual Studio 2017)**  
  
 Si ejecuta el programa de instalación de SSDT en un equipo que ya tiene Visual Studio, solo se agregan las plantillas de proyecto de SQL Server y Business Intelligence. En este escenario se pueden usar las opciones de comentarios del cliente que proporciona Visual Studio para participar o no en el CEIP.  
  
1.  Inicie Visual Studio.  
  
2.  En el menú Ayuda, seleccione **Enviar comentarios** > **Configuración**.  
  
3.  Para desactivar el CEIP, haga clic en **No, no deseo participar**, y, a continuación, haga clic en **Aceptar**.  
  
     Para activar el CEIP, haga clic en **Sí, deseo participar**y, a continuación, haga clic en **Aceptar**.  
  

  
 **Uso de una directiva basada en el Registro o una directiva de grupo**  
  
 Si ejecuta el programa de instalación de SSDT en un equipo que no tiene Visual Studio 2017, solo se instala Visual Studio Shell. El shell no proporciona opciones de comentarios del cliente. En este caso, la única opción para configurar el CEIP es una actualización del Registro.  
  
 Los clientes empresariales pueden crear una directiva de grupo para participar o no estableciendo una directiva basada en el Registro para SQL Server 2017.  
  
 La clave del Registro y la configuración necesarias son:  
  
 Clave = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\15.0\SQM  
  
 Nombre EntradaRegistro = OptIn  
  
 Tipo de entrada DWORD:  
  
-   0 para no utilizar el CEIP  
  
-   1 para utilizarlo  
  
> [!CAUTION]  
>  Una modificación incorrecta del Registro puede provocar daños graves en el sistema. Antes de efectuar cambios en el Registro, debe realizar una copia de seguridad de los datos importantes del equipo. También puede utilizar la opción de inicio La última configuración válida conocida si detecta problemas una vez aplicados los cambios manuales.  
  
 Para obtener más información sobre la información recopilada, procesada o transmitida por el CEIP, consulte la [Declaración de privacidad para el Programa para la mejora de la experiencia del usuario de Microsoft](http://go.microsoft.com/fwlink/?LinkId=52143).  
 
### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>Elección y control sobre el CEIP y SQL Server Data Tools para Visual Studio 2015  
 SSDT para Visual Studio 2015 es la herramienta de modelado de datos incluida en SQL Server 2016. Usa las opciones del CEIP integradas en Visual Studio 2015. Puede obtener más información sobre cómo enviar comentarios a través del CEIP de Visual Studio 2015 en este [documento de ayuda de Visual Studio](http://go.microsoft.com/fwlink/?LinkId=517102).  
  
 En las versiones preliminares de SQL Server 2016, el CEIP está activado de forma predeterminada. Puede desactivarlo o volver a activarlo con las instrucciones siguientes.  
  
 **En Visual Studio (se aplica a las instalaciones de idioma completo de Visual Studio 2015)**  
  
 Si ejecuta el programa de instalación de SSDT en un equipo que ya tiene Visual Studio, solo se agregan las plantillas de proyecto de SQL Server y Business Intelligence. En este escenario se pueden usar las opciones de comentarios del cliente que proporciona Visual Studio para participar o no en el CEIP.  
  
1.  Inicie Visual Studio.  
  
2.  En el menú Ayuda, seleccione **Enviar comentarios** > **Configuración**.  
  
3.  Para desactivar el CEIP, haga clic en **No, no deseo participar**, y, a continuación, haga clic en **Aceptar**.  
  
     Para activar el CEIP, haga clic en **Sí, deseo participar**y, a continuación, haga clic en **Aceptar**.  
  

  
 **Uso de una directiva basada en el Registro o una directiva de grupo**  
  
 Si ejecuta el programa de instalación de SSDT en un equipo que no tiene Visual Studio 2015, solo se instala Visual Studio Shell. El shell no proporciona opciones de comentarios del cliente. En este caso, la única opción para configurar el CEIP es una actualización del Registro.  
  
 Los clientes empresariales pueden crear una directiva de grupo para participar o no si establecen una directiva basada en el Registro para SQL Server 2016.  
  
 La clave del Registro y la configuración necesarias son:  
  
 Clave = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 Nombre EntradaRegistro = OptIn  
  
 Tipo de entrada DWORD:  
  
-   0 para no utilizar el CEIP  
  
-   1 para utilizarlo  
  
> [!CAUTION]  
>  Una modificación incorrecta del Registro puede provocar daños graves en el sistema. Antes de efectuar cambios en el Registro, debe realizar una copia de seguridad de los datos importantes del equipo. También puede utilizar la opción de inicio La última configuración válida conocida si detecta problemas una vez aplicados los cambios manuales.  
  
 Para obtener más información sobre la información recopilada, procesada o transmitida por el CEIP, consulte la [Declaración de privacidad para el Programa para la mejora de la experiencia del usuario de Microsoft](http://go.microsoft.com/fwlink/?LinkId=52143).  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>Elección y control del CEIP y SQL Server Data Tools - BI (SSDT-BI)  
 Si usa SSDT-BI, se le ofrecerá la oportunidad de participar en el CEIP durante la instalación. Más adelante se pueden realizar cambios de configuración del CEIP de SSDT-BI mediante las herramientas de cliente o la edición de la configuración del Registro.  
  
 **En SSDT y SSDT-BI para Visual Studio 2013**  
  
1.  Inicie la herramienta y abra un proyecto nuevo o existente de Analysis Services o Integration Services.  
  
2.  En el menú Ayuda, seleccione **Opciones de comentarios del cliente de Microsoft SQL Server**.  
  
3.  Para desactivar el CEIP, haga clic en **No, no deseo participar**.  
  
     Para activar el CEIP, haga clic en **Sí, deseo participar**.  
  
4.  Haga clic en **Aceptar**.  
  
 **Uso de una directiva basada en el Registro o una directiva de grupo**  
  
 Los clientes empresariales pueden crear una directiva de grupo para participar o no si establecen una directiva basada en el Registro para SQL Server 2014.  
  
 La clave del Registro y la configuración necesarias son:  
  
 Clave = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 Nombre EntradaRegistro = CustomerFeedback  
  
 Tipo de entrada DWORD:  
  
-   0 para no utilizar el CEIP  
  
-   1 para utilizarlo  
  
  
