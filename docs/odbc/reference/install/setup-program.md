---
title: "Programa de instalación | Documentos de Microsoft"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 30637bacfb73d56528233ea13c4c6daeabecf814
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setup-program"></a>Programa de instalación
> **Nota:** a partir de Windows XP y Windows Server 2003, **ODBC se incluye en el sistema operativo Windows**. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 El usuario ejecuta el programa de instalación para iniciar el proceso de instalación. El programa de instalación está escrito por el desarrollador de la aplicación o el controlador. Además de instalar los componentes de ODBC, puede instalar otro software. Por ejemplo, los desarrolladores de aplicaciones pueden utilizar el mismo programa de instalación para instalar los componentes ODBC y para instalar sus aplicaciones.  
  
 Los programadores pueden escribir el programa de instalación desde el principio, mediante el software de instalación de otros proveedores o utilidades de instalación de SDK de Microsoft® Windows®. Esto proporciona a los programadores un control completo sobre la apariencia del programa de instalación. El programa de instalación se puede escribir para instalar software adicional, como una aplicación ODBC. Para obtener más información sobre las utilidades de instalación de SDK de Windows, consulte la documentación del SDK de Windows.  
  
 La cantidad de la instalación se haya realizado realmente por el programa de instalación depende de qué funciones llamadas en el archivo DLL del instalador. El archivo DLL del instalador contiene funciones para instalar los componentes individuales de ODBC. El programa de instalación simplemente llama **SQLInstallDriverManager**, **SQLInstallDriverEx**, o **SQLInstallTranslatorEx** en el instalador de DLL para recuperar la ruta de acceso de la directorio en el que el componente está instalarse y para agregar información sobre el componente en el registro. Estas funciones no realmente copiar los archivos; el programa de instalación hace con la información de los argumentos de estas funciones.  
  
 El archivo DLL del programa de instalación también contiene las funciones para quitar los componentes ODBC. El programa de instalación llame **SQLRemoveDriverManager**, **SQLRemoveDriver**, o **SQLRemoveTranslator** en el instalador de número de DLL para reducir el uso de un componente en el registro y, si el nuevo recuento de uso del componente cae a 0, se quitará toda la información sobre el componente desde el registro. Estas funciones no quitan realmente los archivos de componente; el programa de instalación hace esto si el nuevo recuento de uso cae a 0.
