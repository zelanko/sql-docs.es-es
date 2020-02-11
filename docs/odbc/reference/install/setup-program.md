---
title: Programa de instalación | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc79bb5d12b53938e3e2ef1c531fd03b0002ed78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093830"
---
# <a name="setup-program"></a>Programa de instalación
> **Nota:** A partir de Windows XP y Windows Server 2003, **ODBC se incluye en el sistema operativo Windows**. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 El usuario ejecuta el programa de instalación para iniciar el proceso de instalación. El programa de instalación lo escribe el desarrollador de la aplicación o el controlador. Además de instalar componentes ODBC, puede instalar otro software. Por ejemplo, los programadores de aplicaciones pueden usar el mismo programa de instalación para instalar componentes ODBC e instalar sus aplicaciones.  
  
 Los desarrolladores pueden escribir el programa de instalación desde cero, mediante las utilidades de instalación de Microsoft® Windows® SDK o el software de instalación de otros proveedores. Esto proporciona a los desarrolladores un control completo sobre la apariencia y el funcionamiento del programa de instalación. El programa de instalación se puede escribir para instalar software adicional, como una aplicación ODBC. Para obtener más información acerca de las utilidades de instalación de Windows SDK, consulte la documentación de Windows SDK.  
  
 La cantidad de instalación realizada realmente por el programa de instalación depende de las funciones a las que llama en la DLL del instalador. La DLL del instalador contiene funciones para instalar componentes individuales de ODBC. El programa de instalación simplemente llama a **SQLInstallDriverManager**, **SQLInstallDriverEx**o **SQLInstallTranslatorEx** en el archivo DLL del instalador para recuperar la ruta de acceso del directorio en el que se va a instalar el componente y agregar información sobre el componente al registro. Estas funciones no copian archivos realmente; para ello, el programa de instalación usa la información de los argumentos de estas funciones.  
  
 La DLL del instalador también contiene funciones para quitar componentes ODBC. El programa de instalación llama a **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator** en el archivo DLL del instalador para reducir el recuento de uso de un componente en el registro y, si el nuevo contador de uso del componente cae en 0, quite toda la información sobre el componente del registro. Estas funciones no quitan realmente los archivos para el componente; el programa de instalación lo hace si el nuevo contador de uso cae en 0.
