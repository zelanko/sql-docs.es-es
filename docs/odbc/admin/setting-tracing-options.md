---
title: Configuración de las opciones de seguimiento ( Configuración de las opciones de seguimiento) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21bee5d903459423a134389e62db844f5f63c9c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307206"
---
# <a name="setting-tracing-options"></a>Establecer las opciones de seguimiento
La pestaña **Seguimiento** del cuadro de diálogo Administrador de **orígenes** de datos ODBC permite configurar la forma en que se realiza el seguimiento de las llamadas a funciones ODBC.  
  
## <a name="how-tracing-works"></a>Cómo funciona el seguimiento  
 Al iniciar el seguimiento desde la pestaña **Seguimiento,** el Administrador de controladores registrará todas las llamadas de función ODBC para todas las aplicaciones que se ejecutan posteriormente. Las llamadas a funciones ODBC desde aplicaciones que se ejecutan antes de iniciar el seguimiento no se registran. Las llamadas a funciones ODBC se registran en un archivo de registro que especifique.  
  
 El seguimiento se detiene solo después de hacer clic en **Detener seguimiento ahora**. Recuerde que mientras el seguimiento está activado, el archivo de registro sigue aumentando y que esto afecta al rendimiento de todas las aplicaciones ODBC.  
  
 Para obtener más información sobre el seguimiento, consulte [Seguimiento](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Cambios en el seguimiento ODBC  
 Antes de MDAC 2.7 SP2, solo se permitía que el seguimiento ODBC se produjera en todo el equipo, en el que las capturas de seguimiento exponen detalles sobre todas las aplicaciones ODBC que se ejecutan bajo cualquier identidad. Esto incluía el seguimiento de la actividad relacionada con ODBC que podría producirse para los procesos creados o ejecutados en nombre de otras cuentas de usuario local y entidades de seguridad integradas, como el servicio local y el servicio de red.  
  
 De forma predeterminada, el seguimiento ODBC ahora usa el modo por usuario. Sin embargo, si es un administrador local, puede habilitar el seguimiento de todo el equipo mediante el Administrador de orígenes de datos ODBC.  
  
 Para configurar el modo de seguimiento ODBC:  
  
1.  Si es necesario, inicie sesión con una cuenta que tenga pertenencia al grupo Administradores locales.  
  
2.  En Herramientas administrativas, abra el Administrador de orígenes de datos ODBC.  
  
3.  Haga clic en la pestaña **Seguimiento.**  
  
4.  Configure el modo de seguimiento mediante la casilla de verificación Seguimiento de todo el **equipo para todas las identidades** de usuario:  
  
5.  Para habilitar el seguimiento en todo el equipo, active la casilla de verificación.  
  
6.  Para volver al seguimiento por usuario, desactive la casilla de verificación.  
  
7.  Haga clic en **Aplicar**.  
  
> [!NOTE]  
>  Si ya ha iniciado el seguimiento en un modo, debe detener el seguimiento y cambiar al otro modo para que el modo se cambie correctamente.  
  
> [!IMPORTANT]  
>  El seguimiento de todo el equipo solo debe habilitarse cuando sea necesario; de lo contrario, debe dejarse apagado.  
  
## <a name="visual-studio-analyzer-tracing"></a>Seguimiento de Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  La compatibilidad con Visual Studio Analyzer se quitó a partir de Windows 8 (Visual Studio Analyzer solo se incluía en versiones anteriores de Visual Studio.). Para un mecanismo de solución de problemas alternativo, utilice el seguimiento de BID.  
  
 Seguimiento de Analizador ® Visual Studio proporciona información de rendimiento y depuración sobre la capa ODBC. Todos los eventos salientes se desencadenarán en la interfaz de nivel superior para presentar una imagen lo más precisa posible con respecto al tiempo invertido en componentes ODBC. Seguimiento del analizador de Visual Studio requiere que cualquier origen de eventos se registre cuando se configura el origen. Para obtener más información acerca de este tipo de seguimiento, vea la documentación de Visual Studio.
