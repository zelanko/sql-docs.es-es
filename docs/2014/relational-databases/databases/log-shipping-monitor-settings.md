---
title: Configuración del monitor de trasvase de registros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
ms.openlocfilehash: dcf8810d43f69acc858a0882ad17aa1056014ca7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965935"
---
# <a name="log-shipping-monitor-settings"></a>Configuración del monitor de trasvase de registros
  Utilice esta página para configurar y modificar las propiedades del servidor del monitor de trasvase de registros.  
  
 Para obtener una explicación de los conceptos relacionados con el trasvase de registros, vea [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opciones  
 **Instancia del servidor de supervisión**  
 Muestra el nombre de la instancia del servidor configurado actualmente como el servidor de supervisión para la configuración del trasvase de registros.  
  
 **Conexión**  
 Elija y conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se va a utilizar como servidor de supervisión. La cuenta utilizada para la conexión debe ser miembro del rol fijo de servidor sysadmin en la instancia de servidor secundario.  
  
 **Mediante la suplantación de la cuenta de proxy del trabajo**  
 El trasvase de registros suplanta la cuenta de proxy del Agente SQL Server cuando se conecta a la instancia del servidor de supervisión. Los procesos de copia de seguridad, copia y restauración deben poder conectarse al servidor de supervisión para actualizar el estado de las operaciones de trasvase de registros.  
  
 **Mediante el siguiente inicio de sesión de SQL Server**  
 Permite que el trasvase de registros utilice un inicio de sesión específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se conecta a la instancia del servidor de supervisión. Los procesos de copia de seguridad, copia y restauración deben poder conectarse al servidor de supervisión para actualizar el estado de las operaciones de trasvase de registros. Elija esta opción si desea que el trasvase de registros utilice un inicio de sesión específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y luego especifique el inicio de sesión y la contraseña.  
  
 **Eliminar historial después de**  
 Especifica el intervalo de tiempo que desea mantener la información del historial de trasvase de registros en el servidor de supervisión antes de eliminarla.  
  
 **Nombre del trabajo**  
 Indica el nombre del trabajo de alerta del Agente SQL Server que ha utilizado el trasvase de registros para generar alertas cuando se han superado los límites de copia de seguridad y restauración. Cuando se crea este trabajo por primera vez, se puede cambiar el nombre escribiéndolo en el cuadro.  
  
 **Programación**  
 Indica la programación actual del trabajo de alerta del Agente SQL Server.  
  
 **Edición**  
 Modifique los parámetros del trabajo de alerta del Agente SQL Server.  
  
 **Deshabilitar este trabajo**  
 Suspende el trabajo de alerta del Agente SQL Server.  
  
  
