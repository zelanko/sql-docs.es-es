---
title: Explorador de plantillas | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.templates.explorer.f1
- sql13.wb.templates.f1
helpviewer_keywords:
- templates [SQL Server]
- SQL Server Management Studio [SQL Server], Template Explorer
- Template Explorer
- templates [Transact-SQL]
- templates [SQL Server], Template Explorer
ms.assetid: b9ee55c5-bb44-4f76-90ac-792d8d83b4c8
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e0d0525a7da87f0c2f2363d641fcb07bcd5262ad
ms.lasthandoff: 04/11/2017

---
# <a name="template-explorer"></a>Template Explorer
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] proporciona una variedad de plantillas. Las plantillas son archivos estereotipados que contienen scripts SQL que ayudan a crear objetos en una base de datos. La primera vez que se abre el explorador de plantillas, se coloca una copia de las plantillas en la carpeta del usuario C:\Users, en AppData\Roaming\Microsoft\SQL Server Management Studio\130\Templates.  
  
Puede examinar las plantillas disponibles en el explorador de plantillas; a continuación abra una plantilla para escribir el código en una ventana del editor de código. También puede crear plantillas personalizadas.  
  
## <a name="benefits-of-templates"></a>Ventajas de las plantillas  
Las plantillas están disponibles para las soluciones, los proyectos y diversos tipos de editores de código. Las plantillas están disponibles para crear objetos como bases de datos, tablas, vistas, índices, procedimientos almacenados, desencadenadores, estadísticas y funciones. Además, existen plantillas que ayudan a administrar el servidor al crear propiedades extendidas, servidores vinculados, inicios de sesión, roles, usuarios y plantillas para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)].  
  
Los scripts de las plantillas que se proporcionan con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] contienen parámetros para ayudarle a personalizar el código. Cuando abra una plantilla, use el cuadro de diálogo **Reemplazar parámetros de plantilla** para insertar valores en el script.  
  
Cree plantillas personalizadas para aquellas tareas que realice con frecuencia. Organice los scripts personalizados en las carpetas existentes o cree una nueva estructura de carpetas.  
  
El editor de consultas de [!INCLUDE[ssDE](../../includes/ssde_md.md)] también admite snippets de código que se pueden insertar en ubicaciones concretas de un script haciendo clic con el botón secundario en esa ubicación.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
Use los temas siguientes para empezar a trabajar con las plantillas  
  
|**Description**|**Tema**|  
|-------------------|-------------|  
|Describe cómo incorporar el código de una plantilla en una ventana del editor de código.|[Abrir una plantilla](../../ssms/template/open-a-template.md)|  
|Describe cómo reemplazar valores de parámetros de plantilla después de abrir una plantilla en un editor de código.|[Reemplazar parámetros de plantilla](../../ssms/template/replace-template-parameters.md)|  
  

