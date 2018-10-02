---
title: Versiones en idioma local en SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 20b99363-0490-4aa3-9a3d-262f827d81e8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 914947a72035b5df2247eb01358253938f6eded6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663143"
---
# <a name="local-language-versions-in-sql-server"></a>Versiones en idioma local en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite todos los idiomas compatibles con los sistemas operativos Windows.  
  
## <a name="cross-language-support"></a>Compatibilidad entre idiomas  
  
-   La versión en inglés de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con todas las versiones traducidas de los sistemas operativos.  
  
-   Las versiones localizadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son compatibles con los sistemas operativos con el idioma correspondiente o con las versiones en inglés de los sistemas operativos admitidos mediante la configuración del paquete de Interfaz de usuario multilingüe (MUI) de Windows. Para más información, consulte [Configure Operating System to Support Localized Versions](../../sql-server/install/local-language-versions-in-sql-server.md#BK_ConfigureOS).  
  
-   Las versiones localizadas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo se pueden actualizar a versiones localizadas del mismo idioma y no se pueden actualizar a la versión en inglés.  
  
-   Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también se pueden instalar en paralelo con las instancias en inglés de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="BK_ConfigureOS"></a> Configure Operating System to Support Localized Versions  
 Las versiones traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admiten en las versiones en inglés de los sistemas operativos admitidos a través del uso de la configuración del paquete de Interfaz de usuario multilingüe (MUI) de Windows.  
  
 No obstante, deberá comprobar algunas configuraciones del sistema operativo antes de instalar una versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor que ejecute un sistema operativo en inglés con una configuración de MUI no en inglés. Debe comprobar que las siguientes configuraciones del sistema operativo coinciden con el idioma de la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que vaya a instalar:  
  
-   La configuración de la interfaz de usuario del sistema operativo  
  
-   La configuración regional de usuario del sistema operativo  
  
-   La configuración regional del sistema  
  
 Si la configuración no coincide con el idioma de la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que vaya a instalar, utilice los siguientes procedimientos para establecer correctamente esta configuración del sistema operativo.  
  
> [!CAUTION]  
>  No se admite la instalación de versiones en distinto idioma de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo equipo.  
  
#### <a name="to-change-the-operating-system-user-interface-setting"></a>Para cambiar la configuración de la interfaz de usuario del sistema operativo  
  
1.  Si todavía no está instalada, instale la MUI del sistema operativo que coincide con la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  En Panel de control, abra **Configuración regional y de idioma**.  
  
3.  En la pestaña **Idiomas** , seleccione para **Idioma usado en menús y cuadros de diálogo**, un valor de la lista.  
  
     Este valor afectará al idioma de la interfaz de usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por lo tanto deberá coincidir con la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Haga clic en **Aplicar** para confirmar el cambio y en **Aceptar** para cerrar la ventana.  
  
#### <a name="to-change-the-operating-system-user-locale-setting"></a>Para cambiar la configuración regional de usuario del sistema operativo  
  
1.  Si todavía no está instalada, instale la MUI del sistema operativo que coincide con la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  En Panel de control, abra **Configuración regional y de idioma**.  
  
3.  En la pestaña **Opciones regionales** , en **Seleccionar un elemento para que coincida con sus preferencias**, seleccione un valor de la lista.  
  
     Este valor afectará al formato de los datos específicos de una cultura.  
  
4.  Haga clic en **Aplicar** para confirmar el cambio y en **Aceptar** para cerrar la ventana.  
  
#### <a name="to-change-the-system-locale-setting"></a>Para cambiar la configuración regional del sistema  
  
1.  Si todavía no está instalada, instale la MUI del sistema operativo que coincide con la versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  En Panel de control, abra **Configuración regional y de idioma**.  
  
3.  En la pestaña **Opciones avanzadas** , en **Select a language to match the language version of the non-Unicode programs you want to use**(Seleccione un idioma que coincida con la versión del idioma de los programas no Unicode que quiere usar), seleccione un valor de la lista.  
  
     Este valor permitirá que el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elija la mejor intercalación predeterminada para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
4.  Haga clic en **Aplicar** para confirmar el cambio y en **Aceptar** para cerrar la ventana.  
  
## <a name="see-also"></a>Ver también  
 [Requisitos de hardware y software para instalar SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Instalar SQL Server](../../database-engine/install-windows/install-sql-server.md)  
  
  
