---
title: Plan de mantenimiento (página de informes y registro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 82da951eb38ead64b154b98b138ffd6c0cfaa605
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85024266"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>Plan de mantenimiento (página de informes y registro)
  Use el cuadro de diálogo **Informes y registro** para configurar los informes y registros que se generan al ejecutar los planes de mantenimiento.  
  
## <a name="options"></a>Opciones  
 **Generar un informe de archivo de texto**  
 Especifique si quiere que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escriba un informe de archivo de texto.  
  
 **Crear un nuevo archivo**  
 Crea un nuevo archivo de informe para cada una de las ejecuciones del plan de mantenimiento. De forma predeterminada, los archivos de informe se escriben en el equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene este plan de mantenimiento, en la carpeta establecida como la carpeta de registro predeterminada durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para especificar una carpeta distinta, escriba la ruta de acceso completa de la carpeta en el cuadro de texto **Carpeta** o haga clic en el botón Examinar ( **...** ) y vaya a la carpeta deseada.  
  
 **Anexar a archivo**  
 Anexe el informe de cada ejecución de planes al archivo especificado en el cuadro de texto **Nombre de archivo** . También puede especificar un archivo si hace clic en el botón examinar (&lt;ui&gt;...&lt;/ui&gt;) y selecciona un archivo del cuadro de diálogo.  
  
 **Enviar informe a un destinatario de correo electrónico**  
 Transmite el resultado de la ejecución de un plan de mantenimiento a través de correo electrónico. Esta opción solo estará disponible si el correo electrónico de base de datos se ha habilitado y configurado correctamente.  
  
 **Operador del agente**  
 Seleccione un operador del agente de la lista para que sea destinatario del mensaje de correo electrónico. Esta opción solo estará disponible si el correo se ha habilitado y configurado correctamente.  
  
 **Registrar información adicional**  
 Incluya más información en el registro. Si se incluye esta opción, aumentará el tamaño del historial del plan de mantenimiento almacenado.  
  
 **Registrar en el servidor remoto**  
 Registra el historial del plan de mantenimiento en un servidor remoto.  
  
 **Connection**  
 Especifica la información de conexión que se va a usar al registrar en un servidor remoto.  
  
 **Nuevo**  
 Muestra el cuadro de diálogo **Propiedades de conexión** . Se usa para configurar información de conexión nueva para registrar en un servidor remoto.  
  
## <a name="see-also"></a>Consulte también  
 [Planes de mantenimiento](maintenance-plans.md)   
 [Correo electrónico de base de datos](../database-mail/database-mail.md)  
  
  
