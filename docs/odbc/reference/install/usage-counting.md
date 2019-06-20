---
title: Recuento de uso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca2a52eb08cdf1b1b9cb5a23805da34aab915b7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273391"
---
# <a name="usage-counting"></a>Recuento de uso
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 Dos tipos de recuentos de uso se mantienen en el registro para todos los componentes: un recuento de uso del componente y uno o más recuentos de uso de archivo opcional. El contador de uso del componente ayuda a que el instalador DLL mantener las entradas del registro. Se almacena en el valor UsageCount en el núcleo de ODBC, los controladores y las subclaves de traductor. Para el formato del valor UsageCount y obtener más información sobre estas subclaves, consulte [entradas del registro de componentes de ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Cuando un componente se instala por primera vez, el instalador DLL cuando crea una subclave y establece los datos para el valor UsageCount de dicha subclave en 1. Cuando se instala el componente nuevo, el archivo DLL de instalador incrementa el contador de uso. Cuando se quita el componente, el instalador DLL reduce el uso de recuento. Si el contador de uso cae a 0, el archivo DLL de instalador quita la subclave para el componente.  
  
> [!CAUTION]  
>  Una aplicación no debería quitar físicamente los archivos del Administrador de controladores cuando el recuento de utilización del componente y el recuento de uso de archivo llegue a cero.  
  
 Recuentos de ayudar a determinar si un archivo debe realmente copiar o eliminar como el uso de archivos en lugar de para aumentar o reducir el recuento de uso. Esto es importante porque los componentes de ODBC y, por lo tanto, los archivos de componentes ODBC, se comparten y se pueden instalar o quitar por una variedad de aplicaciones. La aplicación puede eliminar los archivos de controlador y el traductor si el recuento de utilización del componente y el recuento de uso de archivo llegue a cero. Los archivos del Administrador de controladores no se debe, sin embargo, se puede eliminar cuando el recuento de utilización del componente y el recuento de uso de archivo han alcanzado el cero, porque estos archivos se pueden usar otras aplicaciones que no se incrementa el contador de uso de archivo.  
  
> [!NOTE]  
>  Recuentos de uso de archivo son opcionales en Microsoft® WindowsNT®/Windows 2000.  
  
 Recuentos de uso de archivos se mantienen mediante el programa de instalación después de llamar al **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**, o **SQLRemoveTranslator**.  
  
 Cuando un componente se instala por primera vez, el programa de instalación o instalador DLL crea un valor en la siguiente clave para cada archivo en ese componente que no está instalado en el sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  SOFTWARE  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 Establece los datos para esos valores en 1 y copia el archivo en el sistema. Cuando se instala el componente nuevo, el programa de instalación o instalador DLL incrementa los recuentos de uso. Cuando se quita el componente, el disminuye DLL de instalador o programa de instalación el uso de la cuenta. Si cualquier contador de uso cae a 0, el programa de instalación o instalador DLL quita el valor para el archivo y, si el componente es un controlador o un traductor, elimina el archivo. No se deben eliminar los archivos del Administrador de controladores.  
  
 En la tabla siguiente se muestra el formato del valor de recuento de uso del archivo.  
  
|NOMBRE|Tipo de datos|Datos|  
|----------|---------------|----------|  
|*full-path*|REG_DWORD|*Recuento*|  
  
 Por ejemplo, suponga que un controlador para Informix usa los archivos Infrmx32.dll y Infrmx32.hlp y supongamos que este controlador se ha instalado dos veces. Los valores bajo la subclave SharedDlls para el controlador de Informix sería como sigue:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
