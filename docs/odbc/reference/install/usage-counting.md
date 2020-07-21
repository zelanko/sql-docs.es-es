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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296025"
---
# <a name="usage-counting"></a>Recuento de uso
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 En el registro se mantienen dos tipos de recuentos de uso para cada componente: un recuento de uso de componentes y uno o más recuentos de uso de archivos opcionales. El recuento de uso de componentes ayuda al instalador DLL a mantener las entradas del registro. Se almacena en el valor UsageCount en las subclaves ODBC Core, driver y Translator. En el formato del valor UsageCount y más información sobre estas subclaves, vea [entradas del registro para los componentes ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Cuando se instala un componente por primera vez, el archivo DLL del instalador crea una subclave para él y establece los datos del valor UsageCount de esa subclave en 1. Cuando se vuelve a instalar el componente, el archivo DLL del instalador incrementa el recuento de uso. Cuando se quita el componente, el archivo DLL del instalador disminuye el recuento de uso. Si el recuento de uso cae en 0, el archivo DLL del instalador quita la subclave del componente.  
  
> [!CAUTION]  
>  Una aplicación no debe quitar físicamente los archivos del administrador de controladores cuando el recuento de uso de componentes y el recuento de uso de archivos llega a cero.  
  
 Los recuentos de uso de archivos ayudan a determinar cuándo se debe copiar o eliminar un archivo en lugar de incrementar o reducir el recuento de uso. Esto es importante porque los componentes ODBC y, por tanto, los archivos de los componentes ODBC, se comparten y se pueden instalar o quitar en una variedad de aplicaciones. La aplicación puede eliminar archivos de controlador y de traductor si el recuento de uso de componentes y el recuento de uso de archivos llega a cero. No obstante, los archivos del administrador de controladores no deben eliminarse cuando el recuento de uso de componentes y el recuento de uso de archivos alcanzan cero, ya que estos archivos pueden ser usados por otras aplicaciones que no han incrementado el recuento de uso de archivos.  
  
> [!NOTE]  
>  Los recuentos de uso de archivos son opcionales en Microsoft® WindowsNT®/windows2000.  
  
 Los recuentos de uso de archivos son mantenidos por el programa de instalación después de llamar a **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator**.  
  
 Cuando se instala un componente por primera vez, el programa de instalación o el archivo DLL del instalador crea un valor en la clave siguiente para cada archivo de ese componente que todavía no está en el sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  PROGRAMAS  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 Establece los datos de esos valores en 1 y copia el archivo en el sistema. Cuando se vuelve a instalar el componente, el programa de instalación o el archivo DLL del instalador incrementa los recuentos de uso. Cuando se quita el componente, el programa de instalación o el archivo DLL del instalador disminuye los recuentos de uso. Si cualquier recuento de uso cae en 0, el programa de instalación o el archivo DLL del instalador quita el valor del archivo y, si el componente es un controlador o un traductor, elimina el archivo. No se deben eliminar los archivos del administrador de controladores.  
  
 En la tabla siguiente se muestra el formato del valor de recuento de uso de archivo.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*Ruta de acceso completa*|REG_DWORD|*count*|  
  
 Por ejemplo, supongamos que un controlador de Informix usa los archivos Infrmx32. dll y Infrmx32. HLP, y Supongamos que este controlador se ha instalado dos veces. Los valores de la subclave SharedDlls para el controlador de Informix serían los siguientes:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
