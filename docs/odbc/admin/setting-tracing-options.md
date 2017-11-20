---
title: Establecer las opciones de traza | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b11d6337c2e0ca2853838d964842be536454c5f4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setting-tracing-options"></a>Establecer las opciones de traza
El **seguimiento** pestaña de la **Administrador de orígenes de datos ODBC** cuadro de diálogo le permite configurar la forma en que se realice un seguimiento de llamadas a funciones ODBC.  
  
## <a name="how-tracing-works"></a>Cómo funciona el seguimiento  
 Al iniciar el seguimiento de la **seguimiento** ficha, el Administrador de controladores registrará todas las llamadas a funciones ODBC para todos los posteriormente ejecutan las aplicaciones. No se registran las llamadas a funciones ODBC desde aplicaciones que se ejecutan antes de inicia la traza. Llamadas a funciones ODBC se registran en un archivo de registro que especifique.  
  
 Se detiene la traza sólo después de hacer clic en **Detener traza ahora**. Recuerde que mientras el seguimiento está activado, el archivo de registro continúa aumentando y que esto afecta al rendimiento de las aplicaciones de ODBC.  
  
 Para obtener más información acerca del seguimiento, vea [seguimiento](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Cambios en el seguimiento de ODBC  
 Antes de MDAC 2.7 Service Pack 2, seguimiento de ODBC solo se permite que se produzca en una base de todo el equipo, en el que el seguimiento de captura expuestos detalles acerca de todas las aplicaciones de ODBC que se ejecuten en cualquier identidad. Esto incluye el seguimiento de actividad relacionada con ODBC que pudieran producirse en los procesos de crear o ejecutar en nombre de otras cuentas de usuario locales y las entidades de seguridad integradas, como el servicio Local y servicio de red.  
  
 De forma predeterminada, ODBC traza ahora utiliza el modo por el usuario. Sin embargo, si es un administrador local, puede habilitar todavía a seguimiento de todo el equipo mediante el Administrador de orígenes de datos ODBC.  
  
 Para configurar el modo de seguimiento de ODBC:  
  
1.  Si es necesario, inicie sesión con una cuenta que tiene habilitada la pertenencia de grupo de administradores locales.  
  
2.  En Herramientas administrativas, abra el Administrador de orígenes de datos ODBC.  
  
3.  Haga clic en el **seguimiento** ficha.  
  
4.  Configurar el modo de seguimiento mediante la **seguimiento de todo el equipo para todas las identidades de usuario** casilla de verificación:  
  
5.  Para habilitar el seguimiento de todo el equipo, active la casilla de verificación.  
  
6.  Para volver a seguimiento por el usuario, desactive la casilla de verificación.  
  
7.  Haga clic en **Aplicar**.  
  
> [!NOTE]  
>  Si ya ha iniciado el seguimiento en un modo, se deben detener seguimiento e ir al modo para el modo de cambiar correctamente.  
  
> [!IMPORTANT]  
>  Seguimiento de todo el equipo sólo debe habilitarse cuando sea necesario; en caso contrario, debe dejarlo desactivado.  
  
## <a name="visual-studio-analyzer-tracing"></a>Seguimiento del analizador de Visual Studio  
  
> [!IMPORTANT]  
>  Se quitó la compatibilidad con Visual Studio Analyzer a partir de Windows 8 (Visual Studio Analyzer sólo se incluyó en versiones anteriores de Visual Studio.). Para una solución de problemas de mecanismo de forma alternativa, utilizar el seguimiento de BID.  
  
 Seguimiento del analizador de Visual Studio® ofrece rendimiento y la información de depuración sobre la capa de ODBC. Todos los eventos de salida se activarán en la interfaz de nivel superior para presentar una imagen tan precisa como sea posible en cuanto a tiempo invertido en componentes de ODBC. Seguimiento del analizador de Visual Studio requiere cualquier origen de eventos para registrar cuando se configura el origen. Para obtener más información sobre este tipo de seguimiento, consulte la documentación de Visual Studio.

