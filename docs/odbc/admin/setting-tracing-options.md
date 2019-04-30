---
title: Establecer opciones de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ccf5afd559d4d3716c22b42665c516aa230fafe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198525"
---
# <a name="setting-tracing-options"></a>Establecer las opciones de seguimiento
El **seguimiento** pestaña de la **Administrador de orígenes de datos ODBC** cuadro de diálogo le permite configurar la forma en que se realiza un seguimiento de llamadas a funciones ODBC.  
  
## <a name="how-tracing-works"></a>Cómo funciona el seguimiento  
 Al iniciar el seguimiento de la **seguimiento** ficha, el Administrador de controladores registrará todas las llamadas de función ODBC para todos posteriormente ejecutan las aplicaciones. No se registran las llamadas a funciones ODBC desde aplicaciones que se ejecutan antes de inicia el seguimiento. Llamadas a funciones ODBC se registran en un archivo de registro que especifique.  
  
 Se detiene la traza solo después de hacer clic **Detener traza ahora**. Recuerde que aunque el seguimiento está activado, el archivo de registro continúa aumentando y que esto afecta al rendimiento de todas las aplicaciones de ODBC.  
  
 Para obtener más información acerca del seguimiento, vea [seguimiento](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Cambios en el seguimiento de ODBC  
 Antes de MDAC 2.7 Service Pack 2, seguimiento de ODBC solo se permite que se produzca en una base de todo el equipo, en el que seguimiento captura expuesto los detalles sobre todas las aplicaciones ODBC que se ejecutan en ninguna identidad. Esto incluye el seguimiento de actividad relacionada con ODBC que pudieran producirse en los procesos creados o ejecutar en nombre de otras cuentas de usuario locales y las entidades de seguridad integradas, como el servicio Local y servicio de red.  
  
 De forma predeterminada, el seguimiento ahora utiliza el modo por el usuario ODBC. Sin embargo, si es un administrador local, puede habilitar todavía a seguimiento de todo el equipo mediante el Administrador de orígenes de datos ODBC.  
  
 Para configurar el modo de seguimiento de ODBC:  
  
1.  Si es necesario, inicie sesión con una cuenta que tiene pertenencia en el grupo de administradores locales.  
  
2.  En Herramientas administrativas, abra el Administrador de orígenes de datos ODBC.  
  
3.  Haga clic en el **seguimiento** ficha.  
  
4.  Configurar el modo de seguimiento mediante la **seguimiento de todo el equipo para todas las identidades de usuario** casilla de verificación:  
  
5.  Para habilitar el seguimiento de todo el equipo, active la casilla de verificación.  
  
6.  Para volver a seguimiento por el usuario, desactive la casilla de verificación.  
  
7.  Haga clic en **Aplicar**.  
  
> [!NOTE]  
>  Si ya ha iniciado el seguimiento en un modo, deberá detener el seguimiento y cambiar al modo para el modo de cambiar correctamente.  
  
> [!IMPORTANT]  
>  Seguimiento de todo el equipo sólo debe habilitarse cuando sea necesario; en caso contrario, se debe dejar desactivada.  
  
## <a name="visual-studio-analyzer-tracing"></a>Seguimiento del analizador de Visual Studio  
  
> [!IMPORTANT]  
>  Compatibilidad con Visual Studio Analyzer se quitó a partir de Windows 8 (Visual Studio Analyzer sólo se incluyó en versiones anteriores de Visual Studio.). Para conocer una alternativa mecanismo de solución de problemas, use el seguimiento BID.  
  
 Seguimiento del analizador de Visual Studio® proporciona rendimiento y la información de depuración sobre la capa ODBC. Se desencadena todos los eventos de salida en la interfaz de nivel superior para presentar una imagen tan precisa como sea posible en cuanto a tiempo invertido en componentes de ODBC. Seguimiento del analizador de Visual Studio requiere que cualquier origen de eventos para registrar cuando se configura el origen. Para obtener más información sobre este tipo de seguimiento, consulte la documentación de Visual Studio.
