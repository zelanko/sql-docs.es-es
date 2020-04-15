---
title: Programa de configuración ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89cae70db65bd2aa54b8e9789a5c2b35696923e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296155"
---
# <a name="setup-program"></a>Programa de instalación
> **NOTA:** A partir de Windows XP y Windows Server 2003, **ODBC se incluye en el sistema operativo Windows.** Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 El usuario ejecuta el programa de instalación para iniciar el proceso de instalación. El programa de instalación está escrito por el desarrollador de la aplicación o controlador. Además de instalar componentes ODBC, puede instalar otro software. Por ejemplo, los desarrolladores de aplicaciones pueden usar el mismo programa de instalación tanto para instalar componentes ODBC como para instalar sus aplicaciones.  
  
 Los desarrolladores pueden escribir el programa de instalación desde cero, utilizando las utilidades de instalación de Microsoft® Windows® SDK o software de instalación de otros proveedores. Esto da a esos desarrolladores un control completo sobre la apariencia del programa de instalación. El programa de instalación se puede escribir para instalar software adicional, como una aplicación ODBC. Para obtener más información sobre las utilidades de instalación de Windows SDK, consulte la documentación de Windows SDK.  
  
 La cantidad de la instalación se realiza realmente por el programa de instalación depende de qué funciones llama en el archivo DLL del instalador. El archivo DLL del instalador contiene funciones para instalar componentes ODBC individuales. El programa de instalación simplemente llama a **SQLInstallDriverManager**, **SQLInstallDriverEx**o **SQLInstallTranslatorEx** en el archivo DLL del instalador para recuperar la ruta de acceso del directorio en el que se va a instalar el componente y para agregar información sobre el componente al registro. Estas funciones no copian archivos; el programa de instalación hace esto utilizando la información de los argumentos de estas funciones.  
  
 El archivo DLL del instalador también contiene funciones para quitar componentes ODBC. El programa de instalación llama a **SQLRemoveDriverManager**, **SQLRemoveDriver**o **SQLRemoveTranslator** en el archivo DLL del instalador para disminuir el recuento de uso de un componente en el registro y, si el nuevo recuento de uso del componente cae a 0, quitar toda la información sobre el componente del registro. Estas funciones no eliminan realmente los archivos para el componente; el programa de instalación hace esto si el nuevo recuento de uso cae a 0.
