---
title: Mensaje de excepción cuadro programación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ExceptionMessageBox class, about ExceptionMessageBox class
- exception message box [SQL Server], about exception message box
- exception message box [SQL Server]
- interfaces [SQL Server]
- exceptions [SQL Server]
- messages [SQL Server], exception message box
ms.assetid: 0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c
caps.latest.revision: 16
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21882b1f6bb6233723a0ee7b60c7c7682abd5fa7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148376"
---
# <a name="exception-message-box-programming"></a>Programación de cuadros de mensajes de excepción
  El cuadro de mensaje de excepción es una interfaz de programación que se instala y usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes gráficos. El cuadro de mensaje de excepción es un ensamblado administrado compatible que puede usar en sus aplicaciones para proporcionar un control considerablemente mayor sobre la experiencia de mensajería y ofrecer a sus usuarios la opción de guardar el contenido del mensaje de error para hacer referencia al mismo posteriormente y obtener la ayuda sobre los mensajes. Dado que todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalan el cuadro de mensaje de excepción, salvo [!INCLUDE[ssEW](../../includes/ssew-md.md)], puede usarlo sin ninguna configuración adicional en cualquier equipo en el que se hayan instalado los componentes de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La clase <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> del espacio de nombres <xref:Microsoft.SqlServer.MessageBox> incluye toda la funcionalidad de la clase <xref:System.Windows.Forms.MessageBox> y más. La clase <xref:System.Windows.Forms.MessageBox>, que resulta perfecta para cualquier tarea para la que pueda usarse <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>, está diseñada para administrar con elegancia excepciones de código administrado. El cuadro de mensaje de excepción le permite hacer lo siguiente:  
  
-   Proporcionar texto hasta para cinco botones personalizados. Los botones y el cuadro de diálogo cambian de tamaño automáticamente para las distintas longitudes de texto.  
  
-   Permitir que los usuarios copien fácilmente en el Portapapeles el título del mensaje, el texto, el texto del botón y los vínculos de ayuda (si existen) o que envíen esta información en un mensaje de correo electrónico.  
  
-   Mostrar todos los errores y excepciones subyacentes en un árbol de relaciones jerárquicas cuando los usuarios hacen clic **información adicional**.  
  
-   Permitir que los usuarios decidan si debe mostrarse el mensaje cuando vuelva a producirse la misma excepción.  
  
-   Obtener acceso a un sistema de ayuda en pantalla utilizando un vínculo de ayuda asociado con la excepción.  
  
 Para obtener más información, consulte [cuadro de mensaje de excepción de programa](../../../2014/database-engine/dev-guide/program-exception-message-box.md).  
  
  
