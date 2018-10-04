---
title: Administrar archivos con codificación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- files [SQL Server Management Studio]
- encoding [SQL Server Management Studio]
- files [SQL Server Management Studio], encoding
ms.assetid: 919544c9-59f0-4cc6-bb2a-f1ad671eb74b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a30c0ffe6aabe46866d6b2e09b945bc1682898ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095105"
---
# <a name="manage-files-with-encoding"></a>Administrar archivos con codificación
  Para facilitar la visualización del código en un idioma concreto y en una plataforma específica, puede asociar una codificación de caracteres determinada a un archivo.  
  
## <a name="opening-files"></a>Abrir archivos  
 Puede elegir el editor que desea utilizar para modificar el archivo.  
  
#### <a name="to-open-a-file-with-a-specific-editor"></a>Para abrir un archivo con un editor específico  
  
1.  En el menú **Archivo** , seleccione **Abrir**y haga clic en **Archivo**.  
  
2.  En el cuadro de diálogo **Abrir archivo** , seleccione el nombre del archivo.  
  
3.  Haga clic en la flecha situada junto al botón **Abrir** y haga clic en**Abrir con** en el menú que aparece.  
  
4.  En la lista **Seleccione el programa que desee usar** , seleccione un editor y, a continuación, haga clic en **Abrir**. Para abrir el archivo con una codificación determinada, seleccione un editor compatible con la codificación, como el Editor de consultas de SQL con codificación o el Editor XML con codificación.  
  
## <a name="saving-files"></a>Guardar archivos  
 También se puede guardar el código con una codificación Unicode o una página de códigos distinta para que sea compatible con varios idiomas, como europeo occidental o europeo oriental. Puede asociar una codificación de caracteres concreta a un archivo para facilitar la visualización del código en ese idioma, así como un tipo de fin de línea para ser compatible con un sistema operativo determinado. Además, algunos caracteres, cuando se utilizan en los nombres de archivo, no se pueden guardar a menos que se haga con codificación Unicode.  
  
#### <a name="to-save-a-file-with-a-different-encoding-or-line-ending-type"></a>Para guardar un archivo con una codificación o un tipo de fin de línea diferente  
  
1.  En el **archivo** menú, haga clic en **guardar \<filename > como**.  
  
2.  En el cuadro de diálogo **Guardar archivo como** , expanda el botón **Guardar** y, luego, haga clic en **Guardar con codificación**.  
  
3.  En el cuadro de diálogo **Opciones avanzadas para guardar** , seleccione la codificación que desea en la lista **Codificación** .  
  
4.  En la lista **Fin de línea**, seleccione el tipo de fin de línea que desea.  
  
    > [!NOTE]  
    >  Si guarda el archivo con codificación Unicode, éste deberá protegerse en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual SourceSafe como un archivo binario, puesto que este programa no es compatible con la combinación, la comparación ni la comprobación de diferencias entre archivos guardados como Unicode.  
  
 Si utiliza Visual SourceSafe para almacenar archivos con ANSI, UTF8 o Unicode, tenga en cuenta las siguientes limitaciones:  
  
-   Los archivos ANSI solo permiten caracteres compatibles con la página de códigos actual, lo que limita el uso internacional.  
  
-   Los archivos Unicode utilizan la desprotección compartida, la comprobación de diferencias o la funcionalidad de combinación porque se administran como archivos binarios. Este formato se puede utilizar en archivos internacionales.  
  
-   Los archivos UTF8 no funcionan de forma segura con Visual SourceSafe porque los cambios que ocasionan problemas para los editores de archivos UTF8 se realizan durante la protección, la desprotección, la comprobación de diferencias y la combinación.  
  
## <a name="see-also"></a>Vea también  
 [Archivos que administran soluciones y proyectos](files-that-manage-solutions-and-projects.md)   
 [Asociar extensiones de archivo a un editor de código](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)  
  
  
