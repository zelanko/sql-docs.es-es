---
title: Archivos varios | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- files [SQL Server Management Studio], miscellaneous
- projects [SQL Server Management Studio], files
- solutions [SQL Server Management Studio], files
- miscellaneous files folder [SQL Server]
ms.assetid: 3c952b0b-8f5f-4d86-9e5d-616c10b9df0d
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6ea72cab23f488c8330d78dc5c6a1275e043728a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="miscellaneous-files"></a>archivos varios
Los archivos externos a los proyectos se conocen como *archivos varios*. Cuando hay una solución abierta, puede abrir y modificar estos archivos varios relacionados con el proyecto. Un archivo forma parte del grupo de archivos varios si su extensión no está asociada al editor de código del proyecto. Por ejemplo, en un proyecto de scripts de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , los archivos con la extensión .txt o .mdx se tratarán como archivos varios. En un proyecto MDX, los archivos con la extensión .txt o .sql se tratarán como archivos varios. Para asociar una extensión de archivo a un editor de código, consulte [Asociar extensiones de archivo a un editor de código](http://msdn.microsoft.com/en-us/193630f4-93de-4950-8f36-68702531f925).  
  
Existen diversas razones por las que resulta útil poder agregar archivos varios a un proyecto. Puede tener un archivo que no es necesariamente un script reconocido pero que forma parte del desarrollo de la solución. Entre los ejemplos comunes se incluyen notas o instrucciones de desarrollo, archivos de datos y fragmentos de código.  
  
Los archivos varios ofrecen flexibilidad. Por ejemplo, imagine que tiene un proyecto de scripts de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con varios scripts para la creación de tablas y procedimientos almacenados en la base de datos. También tiene varios archivos de datos para las tablas con extensiones .BCP, así como instrucciones de ejecución en un archivo LEAME.TXT. Puede adjuntar los archivos de datos y archivos LEAME al proyecto como archivos varios para aprovechar el control de código fuente y otras características del sistema del proyecto.  
  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] los menús y las barras de herramientas cambian según el formato del archivo que se abra. Por ejemplo, al abrir un archivo de texto, aparece la barra de herramientas Editor de texto. Si se abre un archivo de esquema XML, aparece la barra de herramientas Esquema XML. Mientras se modifica el esquema XML, la barra de herramientas Editor de texto no está disponible. Cuando se pasa de un archivo de proyecto a un archivo perteneciente al grupo de archivos varios, todos los comandos y las barras de herramientas relacionados con el proyecto se sustituyen por los correspondientes al archivo perteneciente al grupo de archivos varios.  
  
## <a name="see-also"></a>Vea también  
[Archivos que administran soluciones y proyectos](../../ssms/solution/files-that-manage-solutions-and-projects.md)  
[Soluciones &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Proyectos &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
  

