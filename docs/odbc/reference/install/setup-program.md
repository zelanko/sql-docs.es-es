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
manager: craigg
ms.openlocfilehash: f64eda5ad640e50afd25db111de74141e41e652d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722153"
---
# <a name="setup-program"></a>Programa de instalación
> **Nota:** a partir de Windows XP y Windows Server 2003, **ODBC se incluye en el sistema operativo Windows**. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 El usuario ejecuta el programa de instalación para iniciar el proceso de instalación. El programa de instalación está escrito por el desarrollador de la aplicación o controlador. Además de instalar los componentes ODBC, puede instalar otro software. Por ejemplo, los desarrolladores de aplicaciones pueden usar el mismo programa de instalación para instalar los componentes ODBC tanto para instalar sus aplicaciones.  
  
 Los desarrolladores pueden escribir el programa de instalación desde cero, con el software de instalación de otros proveedores o utilidades de instalación de SDK de Microsoft® Windows®. Esto proporciona a los desarrolladores control completo sobre la apariencia del programa de instalación. El programa de instalación se puede escribir para instalar software adicional, como una aplicación ODBC. Para obtener más información sobre las utilidades de instalación de Windows SDK, consulte la documentación del SDK de Windows.  
  
 ¿Cuánto de la instalación se realiza realmente el programa de instalación depende de las funciones que se llama en el archivo DLL de instalador. El archivo DLL de instalador contiene funciones para instalar componentes individuales de ODBC. El programa de instalación simplemente llama a **SQLInstallDriverManager**, **SQLInstallDriverEx**, o **SQLInstallTranslatorEx** en el instalador de DLL para recuperar la ruta de acceso de la directorio en el que el componente es instalar y agregar información sobre el componente en el registro. Estas funciones no copie los archivos; realmente el programa de instalación hace esto mediante la información de los argumentos de estas funciones.  
  
 El archivo DLL de instalador también contiene funciones para quitar los componentes ODBC. El programa de instalación llama a **SQLRemoveDriverManager**, **SQLRemoveDriver**, o **SQLRemoveTranslator** en el instalador de recuento de DLL para reducir el uso de un componente el registro y, si el nuevo recuento de uso del componente cae a 0, quitar toda la información sobre el componente del registro. Estas funciones no quitar realmente los archivos para el componente. el programa de instalación no hace esto si el nuevo recuento de uso cae a 0.
