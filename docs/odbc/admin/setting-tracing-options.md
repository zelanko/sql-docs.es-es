---
title: Estableciendo opciones de seguimiento | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307206"
---
# <a name="setting-tracing-options"></a>Establecer las opciones de seguimiento
La pestaña **seguimiento** del cuadro de diálogo **Administrador de orígenes de datos ODBC** le permite configurar la forma en que se realiza el seguimiento de las llamadas a funciones ODBC.  
  
## <a name="how-tracing-works"></a>Cómo funciona el seguimiento  
 Al iniciar el seguimiento desde la pestaña **seguimiento** , el administrador de controladores registrará todas las llamadas a funciones ODBC para todas las aplicaciones que se ejecuten posteriormente. No se registran las llamadas a funciones ODBC desde aplicaciones que se ejecutan antes de iniciar el seguimiento. Las llamadas a funciones ODBC se registran en un archivo de registro que especifique.  
  
 La traza se detiene solo después de hacer clic en **detener seguimiento ahora**. Recuerde que mientras el seguimiento está activado, el archivo de registro continúa aumentando y esto afecta al rendimiento de todas las aplicaciones ODBC.  
  
 Para obtener más información sobre el seguimiento, vea [seguimiento](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Cambios en el seguimiento de ODBC  
 Antes de MDAC 2,7 SP2, el seguimiento de ODBC solo podía realizarse en todo el equipo, en el que seguimiento captura los detalles expuestos sobre todas las aplicaciones ODBC que se ejecutan bajo cualquier identidad. Esto incluye el seguimiento de la actividad relacionada con ODBC que se puede producir para los procesos creados o ejecutados en nombre de otras cuentas de usuario locales y entidades de seguridad integradas, como el servicio local y el servicio de red.  
  
 De forma predeterminada, el seguimiento de ODBC ahora usa el modo por usuario. Sin embargo, si es un administrador local, todavía puede habilitar el seguimiento en todo el equipo mediante el administrador de orígenes de datos ODBC.  
  
 Para configurar el modo de seguimiento de ODBC:  
  
1.  Si es necesario, inicie sesión con una cuenta que tenga la pertenencia al grupo de administradores locales.  
  
2.  En herramientas administrativas, abra el administrador de orígenes de datos ODBC.  
  
3.  Haga clic en la pestaña **seguimiento** .  
  
4.  Configure el modo de seguimiento mediante la casilla **seguimiento en todo el equipo para todas las identidades de usuario** :  
  
5.  Para habilitar el seguimiento en todo el equipo, active la casilla.  
  
6.  Para volver a la traza por usuario, desactive la casilla.  
  
7.  Haga clic en **Aplicar**.  
  
> [!NOTE]  
>  Si ya ha iniciado el seguimiento en un modo, tendrá que detener el seguimiento y cambiar al otro modo para que el modo se cambie correctamente.  
  
> [!IMPORTANT]  
>  La traza en todo el equipo solo se debe habilitar cuando sea necesario; de lo contrario, se debe dejar desactivado.  
  
## <a name="visual-studio-analyzer-tracing"></a>Seguimiento de Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  Se quitó la compatibilidad con Visual Studio Analyzer a partir de Windows 8 (Visual Studio Analyzer solo se incluía en versiones anteriores de Visual Studio). Para un mecanismo de solución de problemas alternativo, use el seguimiento de PUJAs.  
  
 El seguimiento del analizador de® de Visual Studio proporciona información sobre el rendimiento y la depuración sobre el nivel ODBC. Todos los eventos salientes se activarán en la interfaz de nivel superior para presentar una imagen lo más precisa posible con respecto al tiempo empleado en los componentes ODBC. El seguimiento de Visual Studio Analyzer requiere que se registre cualquier origen de eventos cuando se configura el origen. Para obtener más información sobre este tipo de seguimiento, vea la documentación de Visual Studio.
