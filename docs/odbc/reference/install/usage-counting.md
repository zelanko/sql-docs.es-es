---
title: Recuento de usos de la aplicación ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296025"
---
# <a name="usage-counting"></a>Recuento de uso
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 Se mantienen dos tipos de recuentos de uso en el registro para cada componente: un recuento de uso de componentes y uno o varios recuentos de uso de archivos opcionales. El recuento de uso de componentes ayuda a la DLL del instalador a mantener las entradas del Registro. Se almacena en el usageCount valor bajo el ODBC Core, controlador, y las subclaves del traductor. Para obtener el formato del valor UsageCount y más información sobre estas subclaves, vea [Entradas del Registro para componentes ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Cuando se instala un componente por primera vez, el archivo DLL del instalador crea una subclave para él y establece los datos para el UsageCount valor en esa subclave en 1. Cuando el componente se instala de nuevo, el archivo DLL del instalador incrementa el recuento de uso. Cuando se quita el componente, el archivo DLL del instalador disminuye el recuento de uso. Si el recuento de uso cae a 0, el archivo DLL del instalador quita la subclave del componente.  
  
> [!CAUTION]  
>  Una aplicación no debe eliminar físicamente los archivos del Administrador de controladores cuando el recuento de uso de componentes y el recuento de uso de archivos alcanzan cero.  
  
 Los recuentos de uso de archivos ayudan a determinar cuándo se debe copiar o eliminar un archivo en lugar de aumentar o disminuir el recuento de uso. Esto es importante porque los componentes ODBC y, por lo tanto, los archivos de los componentes ODBC, se comparten y pueden instalarse o quitarse mediante una variedad de aplicaciones. La aplicación puede eliminar archivos de controlador y traductor si el recuento de uso de componentes y el recuento de uso de archivos alcanzan cero. Sin embargo, los archivos del Administrador de controladores no se deben eliminar cuando el recuento de uso de componentes y el recuento de uso de archivos han alcanzado cero, ya que estos archivos pueden ser utilizados por otras aplicaciones que no han incrementado el recuento de uso de archivos.  
  
> [!NOTE]  
>  Los recuentos de uso de archivos son opcionales en Microsoft® WindowsNT®/Windows2000.  
  
 El programa de instalación mantiene los recuentos de uso de archivos después de llamar a **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator**.  
  
 Cuando se instala un componente por primera vez, el programa de instalación o DLL del instalador crea un valor bajo la siguiente clave para cada archivo de ese componente que aún no está en el sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  Software  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 Establece los datos de esos valores en 1 y copia el archivo en el sistema. Cuando el componente se instala de nuevo, el programa de instalación o DLL del instalador incrementa los recuentos de uso. Cuando se quita el componente, el programa de instalación o el archivo DLL del instalador disminuyen los recuentos de uso. Si el recuento de uso cae a 0, el programa de instalación o DLL del instalador elimina el valor del archivo y, si el componente es un controlador o un traductor, elimina el archivo. Los archivos del Administrador de controladores no se deben eliminar.  
  
 El formato del valor de recuento de uso de archivos se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*camino completo*|REG_DWORD|*count*|  
  
 Por ejemplo, supongamos que un controlador para Informix utiliza los archivos Infrmx32.dll e Infrmx32.hlp y suponga que este controlador se ha instalado dos veces. Los valores de la subclave SharedDlls para el controlador Informix serían los siguientes:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
