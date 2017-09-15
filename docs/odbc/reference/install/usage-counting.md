---
title: Recuento de uso | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f9db5a35b8b0bb3dc437dd203267c6f53825e22
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="usage-counting"></a>Recuento de uso
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo de Windows. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 Dos tipos de recuentos de uso se mantienen en el registro para cada componente: el contador de uso de un componente y uno o más recuentos de uso de archivo opcional. El contador de uso de componente ayuda a que el instalador DLL mantener las entradas del registro. Se almacena en el valor de UsageCount en el núcleo de ODBC, los controladores y las subclaves de traductor. Con el formato del valor UsageCount y obtener más información sobre estas subclaves, consulte [entradas del registro de componentes de ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Cuando un componente se instala por primera vez, el instalador DLL cuando crea una subclave y establece los datos para el valor de UsageCount de dicha subclave en 1. Cuando se instala el componente nuevo, el instalador DLL incrementa el contador de uso. Cuando se quita el componente, el instalador DLL reduce el uso de recuento. Si el contador de uso cae a 0, el archivo DLL del programa de instalación quita la subclave para el componente.  
  
> [!CAUTION]  
>  Una aplicación no debería quitar físicamente los archivos de administrador de controladores cuando el recuento de utilización del componente y el recuento de uso de archivo llegue a cero.  
  
 Uso del archivo de recuentos de ayudar a determinar si un archivo debe realmente copiar o eliminar como frente al incrementar o disminuir el contador de uso. Esto es importante porque los componentes ODBC y, por lo tanto, los archivos de componentes ODBC, se comparten y pueden deben instalarse o quitarse mediante una variedad de aplicaciones. La aplicación puede eliminar archivos de controlador y el traductor si el contador de uso del componente y el recuento de uso de archivo llegue a cero. Archivos de administrador de controladores no se debe, sin embargo, puede eliminar cuando el recuento de utilización del componente y el recuento de uso de archivo llega a cero, porque estos archivos se pueden usar para otras aplicaciones que no se incrementan el contador de uso de archivo.  
  
> [!NOTE]  
>  Recuentos de uso de archivo son opcionales en Microsoft® WindowsNT®/Windows 2000.  
  
 Recuentos de uso de archivo se mantienen mediante el programa de instalación después de llamar a **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**, o **SQLRemoveTranslator**.  
  
 Cuando se instala un componente por primera vez, el programa de instalación o el instalador DLL crea un valor en la siguiente clave para cada archivo en ese componente que no esté ya en el sistema:  
  
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
  
 Establece los datos para esos valores en 1 y copia el archivo en el sistema. Cuando se instala el componente nuevo, el programa de instalación o el instalador DLL incrementa los recuentos de uso. Cuando se quita el componente, el disminuye DLL de instalador o programa de instalación el uso de la cuenta. Si cualquier contador de uso de cae a 0, el instalador DLL o el programa de instalación quita el valor para el archivo y, si el componente es un controlador o un traductor, elimina el archivo. Archivos de administrador de controladores no se deben eliminar.  
  
 El formato del valor del recuento de uso de archivo se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*ruta de acceso completo*|REG_DWORD|*Recuento*|  
  
 Por ejemplo, supongamos que un controlador para Informix utiliza los archivos Infrmx32.dll y Infrmx32.hlp y supongamos que este controlador se ha instalado dos veces. Los valores bajo la subclave SharedDlls para el controlador de Informix sería como sigue:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
